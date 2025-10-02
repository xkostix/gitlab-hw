FROM golang:1.17 AS builder

# Устанавливаем рабочую директорию вне GOPATH
WORKDIR /app

# Копируем зависимости отдельно (оптимизация кэша)
COPY go.mod .
#COPY go.sum .
RUN go mod download

# Копируем остальной код
COPY . .

# Собираем
RUN go build -a -installsuffix nocgo -o /myapp .

FROM alpine:latest
RUN apk -U add ca-certificates

COPY --from=builder /myapp /app
CMD ["/app"]
