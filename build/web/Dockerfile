# Upstream's Dockerfile (XBEN-005-24/app/Dockerfile) with these changes:
# - the sources are copied from app/app/ (the vendored benchmark folder sits in app/)
# - the build argument FLAG defaults to this lab's fixed flag, the value upstream's Makefile passes
#   (FLAG{sha256 of "XBEN-005-24"}), since the spec passes no build arguments

FROM python:3.12

COPY app/app/ /app

WORKDIR /app

RUN pip install --no-cache-dir -r requirements.txt

ARG FLAG=FLAG{c3aa1ce79de44a89c2cc9598777acd4a950aa054f07b5d1efba2669012be883e}

RUN sed -i s/FLAG/$FLAG/g flag.txt

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]

# CyberCTF per-player flag: the flag above is only the development fallback. ctf-entrypoint.sh
# puts the player's flag (CTF_FLAG_MAIN) in its place at every start, then runs the original
# entrypoint and command, repeated here unchanged.
COPY ctf-entrypoint.sh /usr/local/bin/ctf-entrypoint.sh
ENTRYPOINT ["/usr/local/bin/ctf-entrypoint.sh"]
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
