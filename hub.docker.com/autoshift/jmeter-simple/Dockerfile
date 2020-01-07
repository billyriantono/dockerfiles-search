#    Copyright (C) 2018 Huawei/Futurewei Technologies
#    
#    This Software belongs to the Huawei/Futurewei Technologies. Permission is hereby granted, to the person working on Huawei/Futurewei Technologies projects, including without limitation the rights to use, copy, modify, merge the Software on Huawei/Futurewei Technologies projects.
#    
#    Person cannot use, merge, modify, copy this Software on any project which is not owned by Huawei/Futurewei Technologies.
#    
#    The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

FROM python:3-slim

# Install system packages
RUN pip3 install --upgrade pip &&\
    pip3 install locust&&\
    mkdir /locust/

ENV TARGET=http://127.0.0.1:8080

WORKDIR /locust/

COPY . /locust/

EXPOSE 8089
CMD /usr/local/bin/locust --host=$TARGET -f Users.py --no-reset-stats