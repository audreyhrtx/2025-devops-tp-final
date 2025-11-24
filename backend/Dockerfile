FROM golang:1.24 AS build
WORKDIR /src
COPY . .
RUN go mod download
RUN go build -o server ./cmd/server/main.go

FROM golang:1.24-alpine
WORKDIR /src
COPY --from=build /src/server ./server
COPY --from=build /src/scripts ./scripts
RUN chmod +x ./scripts/migrate.sh
ENV DATABASE_URL="postgres://postgres:postgres@localhost:5432/christmas_gifts?sslmode=disable"
CMD ["./server"]