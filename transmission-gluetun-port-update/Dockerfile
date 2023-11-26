FROM golang:1.21-alpine3.18 as build
COPY root/ /root-layer/

# Install transmission-gluetun-port-update, cache bust if latest commit changed
ADD https://api.github.com/repos/Michsior14/transmission-gluetun-port-update/commits?per_page=1 latest_commit
RUN go install github.com/Michsior14/transmission-gluetun-port-update@latest && \
    mv /go/bin/transmission-gluetun-port-update /root-layer/transmission-gluetun-port-update

FROM scratch
COPY --from=build /root-layer/ /