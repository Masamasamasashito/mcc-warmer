# Microsoft Playwright 
# focal: Ubuntu 20.04 LTS
# jammy: Ubuntu 22.04 LTS
# noble: Ubuntu 24.04 LTS
FROM mcr.microsoft.com/playwright:noble

WORKDIR /app

RUN npm init -y && \
    npm install playwright@latest express && \
    npx playwright install --with-deps

COPY server.js .

ENTRYPOINT ["node", "server.js"]
