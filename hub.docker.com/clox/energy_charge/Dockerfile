FROM python

WORKDIR /home

COPY ./requirment.txt ./
RUN pip install --no-cache-dir -r requirment.txt

COPY . .
CMD ["python", "energy_charge.py"]