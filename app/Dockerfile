# ---- build stage ----
FROM python:3.12-slim AS build
WORKDIR /app
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# ---- final stage ----
FROM python:3.12-slim
WORKDIR /app
COPY --from=build /root/.local /home/appuser/.local
COPY . .
RUN useradd --create-home appuser
USER appuser
ENV PATH=/home/appuser/.local/bin:$PATH
EXPOSE 8000
CMD ["python", "app.py"]
