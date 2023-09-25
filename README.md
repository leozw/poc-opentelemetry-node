# **📊 OpenTelemetry Collector com Docker & Node.js**

Este guia explica como rodar sua aplicação Node.js junto com o OpenTelemetry Collector utilizando Docker.

## **Pré-requisitos**

- Docker e Docker Compose instalados.
- Uma conta no Grafana para obter as credenciais necessárias.

## **Configurando e Executando com Docker 🐳**

### **1. Arquivo de configuração do OpenTelemetry Collector:**

- Abra ou crie o arquivo **`otel-collector-config.yaml`** no seu diretório.
- Substitua o **`endpoint`** e o cabeçalho **`Authorization`** com suas próprias credenciais do Grafana:

```yaml
otlp:
  endpoint: https://YOUR_GRAFANA_TEMPO_ENDPOINT
  headers:
    Authorization: Basic CONVERTED_TO_BASE64 (INSTANCEID:APIKEY) 
prometheusremotewrite:
  endpoint: https://INSTANCEID:APIKEY@YOUR_GRAFANA_PROMETHEUSREMOTEWRITE_ENDPOINT

```

🚀 **Atenção**: Converta suas credenciais do Grafana para Base64 e use no lugar de **`CONVERTED_TO_BASE64`**. Para o **`prometheusremotewrite`**, não precisa da conversão.

### **2. Preparação do Dockerfile:**

Seu Dockerfile está pronto para construir a imagem da sua aplicação em um ambiente Node.js. Lembre-se que ele expõe a porta **`9191`**.

### **3. Construindo e Executando com Docker Compose:**

- Com base no diretório onde o **`docker-compose.yml`** está localizado, construa as imagens Docker:

```bash
docker-compose build

```

- Após a construção, inicie os serviços:

```bash
docker-compose up

```

- Agora, acesse sua aplicação no navegador através da URL: **`http://localhost:9191`**.
- Depois de testar, pare os serviços:

```bash
docker-compose down

```

---

Com isso, sua aplicação Node.js estará rodando junto com o OpenTelemetry Collector no Docker, e estará enviando dados de telemetria para o Grafana. Se encontrar qualquer problema ou tiver alguma sugestão, não hesite em contribuir! 🚀
