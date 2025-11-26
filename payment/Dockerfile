# --------------------------
#   BUILDER STAGE
# --------------------------
# FROM python:3.9.25-alpine3.21 AS builder

# WORKDIR /install

# # Build dependencies
# RUN apk add --no-cache build-base linux-headers pcre-dev

# # Install Python packages into /install
# COPY requirements.txt .
# RUN pip install --prefix=/install -r requirements.txt



# # --------------------------
# #   FINAL RUNTIME STAGE
# # --------------------------
# FROM python:3.9.25-alpine3.21

# EXPOSE 8080
# WORKDIR /opt/server

# # Runtime deps only
# RUN apk add --no-cache pcre

# # Create non-root user
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# # Copy installed packages from builder
# COPY --from=builder /install /usr/local

# # Copy application files
# COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt .

# # Environment Variables
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"

# USER roboshop

# CMD ["uwsgi", "--ini", "payment.ini"]


FROM python:3.9
EXPOSE 8080
WORKDIR /opt/server
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip3 install -r requirements.txt
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uwsgi","--ini","payment.ini"]