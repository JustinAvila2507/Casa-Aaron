FROM python:3.12-slim

# Instalar las librerías del sistema que pide WeasyPrint a gritos
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3-dev \
    libpango-1.0-0 \
    libharfbuzz0b \
    libpangoft2-1.0-0 \
    libpangocairo-1.0-0 \
    libgdk-pixbuf2.0-0 \
    libglib2.0-0 \
    shared-mime-info \
    libcairo2 \
    default-libmysqlclient-dev \
    default-mysql-client \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copiar e instalar dependencias de Python
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar el resto del proyecto
COPY . .

# Comando para ejecutar la aplicación usando la ruta correcta
CMD ["gunicorn", "Proyecto_Arron_Django.arrons.wsgi:application", "--bind", "0.0.0.0:$PORT"]