FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    procps \
    iproute2 \
    iputils-ping \
    net-tools \
    vim \
    python3 \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/apt/keyrings && \
    curl -fsSL https://packages.wazuh.com/key/GPG-KEY-WAZUH \
    | gpg --dearmor -o /etc/apt/keyrings/wazuh.gpg && \
    chmod 644 /etc/apt/keyrings/wazuh.gpg && \
    echo "deb [signed-by=/etc/apt/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" \
    > /etc/apt/sources.list.d/wazuh.list

RUN apt-get update && \
    apt-get install -y wazuh-agent=4.14.10-1 && \
    apt-mark hold wazuh-agent && \
    rm -rf /var/lib/apt/lists/*

RUN python3 - <<'PY'
import re
from pathlib import Path

path = Path("/var/ossec/etc/ossec.conf")
text = path.read_text()
match = re.search(r"<client>.*?</client>", text, flags=re.S)
if not match:
    raise SystemExit("ERROR: client block not found")

client = match.group(0)
client, count = re.subn(r"<address>.*?</address>",
    "<address>wazuh.manager</address>", client, count=1, flags=re.S)
if count != 1:
    raise SystemExit("ERROR: manager address not found")

enrollment = [
    "    <enrollment>",
    "      <enabled>yes</enabled>",
    "      <agent_name>linux-endpoint-01</agent_name>",
    "      <manager_address>wazuh.manager</manager_address>",
    "      <port>1515</port>",
    "    </enrollment>"
]
enrollment_xml = "\n".join(enrollment)

if re.search(r"<enrollment>.*?</enrollment>", client, flags=re.S):
    client = re.sub(r"<enrollment>.*?</enrollment>",
        lambda _: enrollment_xml, client, count=1, flags=re.S)
else:
    client = client.replace("</client>",
        enrollment_xml + "\n  </client>", 1)

text = text[:match.start()] + client + text[match.end():]
path.write_text(text)
PY

CMD ["/bin/bash"]
