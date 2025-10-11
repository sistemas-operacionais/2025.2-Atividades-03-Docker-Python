# Relato de Aaron Guerra Goldberg sobre a Atividade - Docker com Python

## 6.1 Introdução
Esta atividade teve como objetivo principal aprender a criar e executar containers Docker com Python, utilizando a plataforma Docker para isolar ambientes de execução. O Docker permite que aplicativos sejam executados em containers independentes, garantindo consistência entre desenvolvimento e produção. 

O uso do Docker com Python nesta atividade foi importante para compreender conceitos de:  
- **Docker e containers**: ambientes isolados que contêm todas as dependências de uma aplicação.  
- **Dockerfile**: arquivo que define como a imagem do container será construída.  
- **Mapeamento de volumes**: permite que alterações feitas nos arquivos do host sejam refletidas dentro do container em tempo real.

---

## 6.2 Atividades Realizadas
### Parte 1: Preparação do Repositório
- Realizei o **fork** do repositório oficial da atividade no GitHub.  
- Clonei o repositório forkado para o Codespace:  
```bash
git clone https://github.com/SEU_USUARIO/2025.2-Atividades-03-Docker-Python.git
cd 2025.2-Atividades-03-Docker-Python
```

### Parte 2: Criação dos Arquivos Python
- Criei o arquivo `alomundo.py`:
```python
print("Alô, Mundo!")
print("Bem-vindo ao container Docker com Python!")
print("Sistemas Operacionais - 2025.2")
```
- Criei o arquivo `calculadora.py`:
```python
def somar(a, b):
    return a + b

def subtrair(a, b):
    return a - b

def multiplicar(a, b):
    return a * b

def dividir(a, b):
    if b != 0:
        return a / b
    else:
        return "Erro: Divisão por zero!"

print("=== Calculadora Simples ===")
print(f"10 + 5 = {somar(10, 5)}")
print(f"10 - 5 = {subtrair(10, 5)}")
print(f"10 * 5 = {multiplicar(10, 5)}")
print(f"10 / 5 = {dividir(10, 5)}")
```

### Parte 3: Criação do Dockerfile
- Criei o arquivo `Dockerfile`:
```dockerfile
FROM fedora:latest
RUN dnf install -y python3 python3-pip && dnf clean all
RUN mkdir -p /app
WORKDIR /app
CMD ["python3"]
```

### Parte 4: Construção e Execução do Container
- Construí a imagem Docker:
```bash
docker build -t python-fedora-app .
```

- Verifiquei se a imagem foi criada:
```bash
docker images | grep python-fedora-app
```

- Executei o `alomundo.py` dentro do container:
```bash
docker run --rm -v $(pwd):/app python-fedora-app python3 /app/alomundo.py
```

- Executei o `calculadora.py` dentro do container:
```bash
docker run --rm -v $(pwd):/app python-fedora-app python3 /app/calculadora.py
```

- Testei o mapeamento de volumes editando `alomundo.py` e executando novamente, confirmando que a alteração foi refletida no container.

### Parte 5: Versionamento no GitHub
- Adicionei e commit os arquivos no Git:
```bash
git add Dockerfile alomundo.py calculadora.py
git commit -m "Adiciona Dockerfile e programas Python"
git push origin main
```

---

## 6.3 Considerações Finais
- **Principais dificuldades:**  
  - Configuração do mapeamento de volumes no Codespace.  
  - Alertas do `dnf` durante a instalação do Python no Fedora, sem impedir a execução.  

- **Aprendizados:**  
  - Entendi a importância do Docker para manter ambientes consistentes.  
  - Aprendi a rodar scripts Python dentro de containers e a editar arquivos com volume compartilhado.  

---

**Conclusão:**  
A atividade permitiu aplicar na prática conceitos fundamentais de Docker, construção de imagens, execução de containers e integração com arquivos Python, fortalecendo habilidades importantes para desenvolvimento e operação de sistemas isolados.
