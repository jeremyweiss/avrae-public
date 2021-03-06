FROM tiangolo/uwsgi-nginx:python3.6

# By default, allow unlimited file sizes, modify it to limit the file sizes
# To have a maximum of 1 MB (Nginx's default) change the line to:
# ENV NGINX_MAX_UPLOAD 1m
ENV NGINX_MAX_UPLOAD 1m

# Which uWSGI .ini file should be used, to make it customizable
ENV UWSGI_INI /web/uwsgi.ini

# URL under which static (not modified by Python) files will be requested
# They will be served by Nginx directly, without being handled by uWSGI
ENV STATIC_URL /static
# Absolute path in where the static files wil be
ENV STATIC_PATH /web/static

# If STATIC_INDEX is 1, serve / with /static/index.html directly (or the static URL configured)
# ENV STATIC_INDEX 1
ENV STATIC_INDEX 0

# Copy the entrypoint that will generate Nginx additional configs
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

# Copy the current directory contents into the container at /web
COPY . /web
# Set the working directory to /app
WORKDIR /web

# Install any needed packages specified in requirements.txt
RUN pip3.6 install -r requirements.txt

EXPOSE 80

CMD ["/usr/bin/supervisord"]