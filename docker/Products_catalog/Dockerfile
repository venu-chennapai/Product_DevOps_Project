FROM golang:1.22-alpine AS builder
WORKDIR /user/src/app
COPY . .
RUN go build -o product-catalog ./

FROM alpine AS release
WORKDIR /user/src/app
COPY ./products ./products
COPY --from=builder /user/src/app/product-catalog ./
EXPOSE  ${PRODUCT_CATALOG_PORT}
ENTRYPOINT [ "/user/src/app/product-catalog" ]
