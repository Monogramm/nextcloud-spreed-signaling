FROM alpine:3.11

RUN apk add --no-cache coturn

CMD ["turnserver", "--prod", "--fingerprint", "--use-auth-secret", "--lt-cred-mech", "--static-auth-secret=$STATIC_SECRET", "--realm=$REALM", "--no-multicast-peers", "--no-tls", "--no-dtls"]
