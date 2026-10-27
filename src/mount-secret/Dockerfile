FROM alpine

ARG REPO_PATH=github.com/username/repository.git

RUN apk add --no-cache git

# clone the repository
RUN --mount=type=secret,id=github_token,env=GITHUB_TOKEN \
    git clone https://github_user:$GITHUB_TOKEN@REPO_PATH /app

RUN chmod +x /app/script.sh

CMD ["/app/script.sh"]
