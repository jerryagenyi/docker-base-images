FROM selenium/standalone-chrome

# Install Python and pip
USER root
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Install common testing packages
RUN pip3 install --no-cache-dir \
    selenium \
    pytest \
    pytest-selenium \
    pytest-html \
    pytest-xdist \
    allure-pytest \
    webdriver-manager \
    requests

WORKDIR /app

# Script to handle test execution
COPY <<-"EOT" /app/run-tests.sh
#!/bin/bash
if [ -f requirements.txt ]; then
    pip3 install -r requirements.txt
fi

if [ -f "pytest.ini" ]; then
    pytest "$@"
else
    pytest --html=report.html --self-contained-html "$@"
fi
EOT

RUN chmod +x /app/run-tests.sh

# Switch back to selenium user for security
USER seluser

ENTRYPOINT ["/app/run-tests.sh"]
CMD ["test_script.py"]