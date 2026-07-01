FROM python:3.12-slim

# 1. Instalar las librerías del sistema operativo que WeasyPrint necesita para los reportes
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

# 2. Copiar e instalar los requerimientos de Python
# Apuntamos a la ruta real de tu archivo dentro del repositorio
COPY Proyecto_Arron_Django/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 3. Copiar todo el proyecto al servidor
COPY . .

# 4. Cambiar el directorio de trabajo a donde está el manage.py para que los comandos funcionen directo
WORKDIR /app/Proyecto_Arron_Django

# 5. Comando para arrancar el servidor con Gunicorn apuntando al WSGI correcto
CMD ["gunicorn", "arrons.wsgi:application", "--bind", "0.0.0.0:$PORT"]