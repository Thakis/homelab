services:
    speedtest-tracker:
        image: lscr.io/linuxserver/speedtest-tracker:latest
        restart: unless-stopped
        container_name: speedtest-tracker
        ports:
            - 8080:80
            - 8443:443
        environment:
            - PUID=1000
            - PGID=1000
            - APP_KEY=APP_KEY
            - DB_CONNECTION=sqlite
            - APP_TIMEZONE=Europe/Berlin
            - SPEEDTEST_SCHEDULE=6 */2 * * *
        volumes:
            - /path/to/data:/config
            - /path/to-custom-ssl-keys:/config/keys