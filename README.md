# 🧪 Testes de API - ServeRest

Projeto de testes manuais de API desenvolvido com **Insomnia** utilizando a API pública [ServeRest](https://serverest.dev), simulando um e-commerce com usuários, produtos e carrinhos.

---

## 🛠️ Ferramentas utilizadas

- [Insomnia](https://insomnia.rest/) — client para testar requisições HTTP
- [ServeRest API](https://serverest.dev) — API REST gratuita para prática de testes
- JSON — formato de envio e recebimento dos dados

---

## 📋 Endpoints testados

### 👤 Usuários
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/usuarios` | Criar novo usuário |
| GET | `/usuarios` | Listar todos os usuários |
| GET | `/usuarios/{id}` | Buscar usuário por ID |
| PUT | `/usuarios/{id}` | Editar usuário |
| DELETE | `/usuarios/{id}` | Deletar usuário |

### 🔐 Login
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/login` | Autenticar usuário e obter token Bearer |

### 📦 Produtos
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/produtos` | Criar produto (requer token) |
| GET | `/produtos` | Listar todos os produtos |
| GET | `/produtos/{id}` | Buscar produto por ID |
| PUT | `/produtos/{id}` | Editar produto |
| DELETE | `/produtos/{id}` | Deletar produto |

### 🛒 Carrinhos
| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/carrinhos` | Cadastrar carrinho (requer token) |
| GET | `/carrinhos` | Listar carrinhos cadastrados |
| GET | `/carrinhos/{id}` | Listar carrinho por ID |
| DELETE | `/carrinhos/concluir-compra` | Excluir carrinho e finalizar compra |
| DELETE | `/carrinhos/cancelar-compra` | Excluir carrinho e retornar produtos |

---

## 🔄 Fluxo de autenticação

Algumas rotas exigem autenticação via **Bearer Token**. O fluxo utilizado foi:

```
1. POST /usuarios  → criar usuário
2. POST /login     → autenticar e receber o token
3. Usar o token no Header Authorization das próximas requisições
```

O script abaixo foi configurado no **Post-response** do Login para salvar o token automaticamente como variável de coleção:

```javascript
let jsonResp = pm.response.json();
let jsonToken = jsonResp['authorization'].split('Bearer ');
pm.collectionVariables.set("user_token", jsonToken[1]);
```

---

## ✅ Cenários testados

- Criar usuário com dados válidos → `201 Created`
- Criar usuário com email já cadastrado → `400 Bad Request`
- Login com credenciais válidas → `200 OK` + token
- Login com credenciais inválidas → `401 Unauthorized`
- Buscar usuário por ID existente → `200 OK`
- Buscar usuário por ID inexistente → `400 Bad Request`
- Criar produto sem token → `401 Unauthorized`
- Criar produto com token válido → `201 Created`
- Cadastrar carrinho com produto existente → `201 Created`

---

## 📁 Como importar no Insomnia

1. Baixe o arquivo `serverest-collection.json` deste repositório
2. Abra o Insomnia
3. Clique em **Import** → selecione o arquivo
4. Configure a variável `BASE_URL` com `https://serverest.dev`

---

## 👨‍💻 Autor

**Wilker Fonseca**  
Estudante de QA | Testes de API  
[LinkedIn](https://www.linkedin.com/in/wilker-fonseca-martiniano-16a436159/) • [GitHub](https://github.com/wilker02)
