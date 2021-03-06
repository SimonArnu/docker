FROM java:8-jre

ENV JYTHON_VERSION 2.7.0

RUN curl -Lo jython-installer-${JYTHON_VERSION}.jar "http://search.maven.org/remotecontent?filepath=org/python/jython-installer/2.7.0/jython-installer-2.7.0.jar" \
    && java -jar jython-installer-${JYTHON_VERSION}.jar -s -t minimum -i mod -d /usr/share/jython-${JYTHON_VERSION} \
    && rm -f jython-installer-${JYTHON_VERSION}.jar

# Latest virtualenv to work with 2.5.x is 15.1.0 (2013-03-08)
# and brings easy_install and pip along with it
RUN curl -O  https://pypi.python.org/packages/d4/0c/9840c08189e030873387a73b90ada981885010dd9aea134d6de30cd24cb8/virtualenv-15.1.0.tar.gz \
    && tar xzf virtualenv-15.1.0.tar.gz \
    && cd virtualenv-15.1.0 \
    && /usr/share/jython-${JYTHON_VERSION}/bin/jython setup.py install \
    && ln -s /usr/share/jython-${JYTHON_VERSION}/bin/virtualenv /usr/local/bin/ \
    && cd .. \
    && rm -rf virtualenv-15.1.0 \
    && rm -f virtualenv-15.1.0.tar.gz

RUN virtualenv /usr/src \
    && ln -s /usr/src/bin/* /usr/local/bin/

ENV VIRTUAL_ENV /usr/src

# Add jip to support Java dependencies
RUN pip install jip==0.9.13 \
    && ln -s /usr/src/bin/jip /usr/local/bin/ \
    && ln -s /usr/src/bin/jython-all /usr/local/bin/

CMD ["jython-all"]
