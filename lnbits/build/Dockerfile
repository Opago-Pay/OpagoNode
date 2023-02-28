FROM python:3.9-slim

RUN apt-get clean
RUN apt-get update
RUN apt-get install -y curl pkg-config build-essential git
RUN curl -sSL https://install.python-poetry.org | python3 -

ENV PATH="/root/.local/bin:$PATH"

RUN git clone https://github.com/lnbits/lnbits/ /app

WORKDIR /app
RUN mkdir -p lnbits/data

RUN poetry config virtualenvs.create false
RUN poetry install --only main
RUN poetry run python tools/build.py

ENV LNBITS_PORT="5000"
ENV LNBITS_HOST="0.0.0.0"
ENV LNBITS_SITE_TITLE="OPAGO LNbits"
ENV LNBITS_SITE_TAGLINE="OPAGO version of the LNbits free and open-source lightning wallet"
ENV LNBITS_THEME_OPTIONS="monochrome"
ENV LNBITS_CUSTOM_LOGO="https://i0.wp.com/opago-pay.com/wp-content/uploads/2022/07/opago-logo-1024x1024-1.png?w=3240"
ENV LNBITS_BACKEND_WALLET_CLASS=LndWallet
ENV LND_GRPC_ENDPOINT=lnd
ENV LND_GRPC_PORT=10009
ENV LND_GRPC_CERT="/root/.lnd/tls.cert"
ENV LND_GRPC_MACAROON="/root/.lnd/data/chain/bitcoin/mainnet/admin.macaroon"
ENV LNBITS_ADMIN_EXTENSIONS="ngrok, admin, user manager"

CMD ["sh", "-c", "poetry run lnbits --port $LNBITS_PORT --host $LNBITS_HOST"]
