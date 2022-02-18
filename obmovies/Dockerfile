FROM python:3.6
# add files
ADD . /obmovies
# set workdir
WORKDIR /obmovies
# install requirements
RUN pip install -r requirements.txt
# use port for the app
EXPOSE 5000
#run command
CMD ["python", "run.py"]
