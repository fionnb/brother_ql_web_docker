FROM opensuse:42.3

RUN zypper mr -Ka \
 && zypper ref \
 && zypper --non-interactive install \
 # Install some fonts
      fifth-leg-font \
      fontconfig \
      git \
      python3 \
      python3-bottle \
      python3-devel \
      python3-Jinja2 \
 # we need a newer version (this would install 2.9.0):
 #    python3-Pillow \
      python3-pip

# change default python
RUN rm /usr/bin/python /usr/bin/pip \
 && ln -s /usr/bin/python3 /usr/bin/python \
 && ln -s /usr/bin/pip3 /usr/bin/pip

# upgrade pip (latest version gets binary wheels mostly)
RUN pip install --no-cache-dir --upgrade pip

RUN git clone https://github.com/pklaus/brother_ql_web.git
WORKDIR ./brother_ql_web
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8013

#CMD [ "brother_ql_create", "--help" ]
CMD [ "./brother_ql_web.py", "--model", "QL-700", "file:///dev/usb/lp0" ]
