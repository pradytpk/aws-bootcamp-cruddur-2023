FROM python:3.10-slim-buster

#Inside container
# make a new folder inside container
WORKDIR /backend-flask
#outside container -> Inside Container
# this contains the libraries want to install to run the app
COPY requirements.txt requirements.txt
#Inside container
#Install the python libraries used for the app
RUN pip3 install -r requirements.txt

#outside container -> Inside Container
# . means everything in the current container
# first period ./backend-flask(outside container)
# second period  ./backend-flask(Inside container)
COPY . .

# set rnv variables
# inside the container and will remain set when the container is running
ENV FLASK_ENV=development

EXPOSE ${PORT}
# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]