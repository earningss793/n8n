FROM n8nio/base:22

# 1) 필요한 패키지들
RUN apk add --no-cache --update \
    openssh \
    sudo \
    shadow \
    bash

# 2) node 사용자에게 sudo 권한
RUN echo "node ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/node \
 && chmod 0440 /etc/sudoers.d/node

# 3) 작업 디렉토리 준비
RUN mkdir /workspaces && chown node:node /workspaces

USER node

RUN mkdir -p ~/.pnpm-store \
 && pnpm config set store-dir ~/.pnpm-store --global

# 4) n8n 글로벌 설치
#    (원하시면 특정 버전(@latest), 또는 @0.282.0 같이 지정도 가능합니다)
RUN npm install -g n8n

# 5) 컨테이너 시작 시 n8n 서버 실행
CMD ["n8n", "start"]
