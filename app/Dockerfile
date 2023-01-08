FROM python:3.11-slim as dev

# Setup vim
RUN apt-get update

RUN apt-get install -y vim curl

RUN mkdir -p ~/.vim/colors/ && \
    curl https://raw.githubusercontent.com/joshdick/onedark.vim/main/colors/onedark.vim >> ~/.vim/colors/onedark.vim && \
    mkdir -p ~/.vim/autoload/ && \
    curl https://raw.githubusercontent.com/joshdick/onedark.vim/main/autoload/onedark.vim >> ~/.vim/autoload/onedark.vim
    
WORKDIR /usr/src/app

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# ENTRYPOINT /bin/bash
# CMD [ "python", "./your-daemon-or-script.py" ]
CMD [ "flask", "--debug", "run", "--host=0.0.0.0" ]



FROM python:3.11-alpine as prod

WORKDIR /usr/src/app

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# ENTRYPOINT /bin/bash
# CMD [ "python", "./your-daemon-or-script.py" ]
CMD [ "flask", "run", "--host=0.0.0.0" ]
