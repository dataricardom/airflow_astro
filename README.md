# Projeto Airflow com Astro CLI + Docker

Este projeto utiliza o **Astro CLI** para subir um ambiente de desenvolvimento com o **Apache Airflow**, utilizando containers Docker.

## 🔧 Requisitos

- Docker instalado e rodando no sistema
- Astro CLI instalado
- Linux (Fedora, no meu caso)

## 🚀 Configuração

O ambiente foi iniciado com o comando:

```bash
astro dev init
```

E executado com:

```bash
astro dev start
```

## ⚠️ Ajuste necessário para evitar erro com QEMU

Por padrão, o Astro CLI pode tentar usar o engine `qemu` ao invés do Docker, especialmente se ele não encontrar o Docker corretamente ou se não estiver configurado explicitamente.

Isso pode causar o seguinte erro ao tentar iniciar o projeto:

```
running engine: engine linux/qemu failed to run: running VM: running virtiofsd for /home: signal: bad system call (core dumped)
```

### ✅ Solução aplicada

Para resolver o problema, foi necessário forçar o Astro CLI a usar o **engine Docker**:

```bash
export ASTRO_ENGINE=docker
astro dev start
```

> **Dica:** Para tornar isso permanente, adicione ao seu `~/.bashrc` ou `~/.zshrc`:

```bash
export ASTRO_ENGINE=docker
```

## 📁 Estrutura básica do projeto

```text
.
├── dags/                  # Onde ficam as DAGs do Airflow
├── Dockerfile             # Imagem customizada (se necessário)
├── include/               # Arquivos auxiliares, scripts SQL etc.
├── plugins/               # Plugins personalizados do Airflow
├── requirements.txt       # Dependências adicionais do projeto
└── .astro/                # Configurações internas do Astro CLI
```

## 🧪 Testando DAGs

Basta adicionar arquivos `.py` com DAGs no diretório `dags/`. O Airflow carregará automaticamente sem a necessidade de reiniciar o container (modo dev ativo).

## 📌 Observações

- O PostgreSQL interno do Airflow usa a porta padrão `5432`. Se já houver outro PostgreSQL rodando, edite o `docker-compose.override.yml` para evitar conflito de portas.

## ✅ Status

✅ Ambiente funcionando com Astro CLI e Docker  
✅ DAGs detectadas automaticamente  
✅ Conexões testadas com sucesso no Airflow UI

---

Criado por Ricardo Marques
