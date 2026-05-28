# E-COMMERCE AI - Backend de Busca Semântica Vetorial

Este projeto consiste no desenvolvimento do ecossistema de backend para um e-commerce inteligente. O grande diferencial técnico é a substituição da busca tradicional por palavras-chave (SQL Like) por uma **Busca Semântica (Vetorial)** utilizando Inteligência Artificial e Banco de Dados Vetorial.

## Como Funciona a Busca Semântica?
Em vez de buscar termos exatos, o sistema utiliza o modelo de Processamento de Linguagem Natural (NLP) da biblioteca **Transformers.js** para converter as descrições dos produtos em vetores numéricos de alta dimensão (Embeddings). Esses vetores capturam o *significado* e o *contexto* do texto. 

Quando o usuário faz uma busca, a sua frase também virá um vetor, e o **Pinecone** calcula a distância matemática entre eles, trazendo os produtos mais relevantes mesmo que o usuário use sinônimos ou descreva uma situação (ex: buscar "roupa para frio" e o sistema retornar um "Moletom" ou "Gorro").

## Tecnologias Utilizadas
- **Ambiente de Execução:** Node.js
- **Framework Web:** Express (API REST)
- **Banco de Dados Vetorial:** Pinecone (nuvem)
- **Modelos de IA / Embeddings:** Transformers.js (Hugging Face)
- **Comunicação HTTP:** Axios & CORS
- **Segurança:** Dotenv (Gerenciamento de chaves de API ocultas)

## Rotas da API (Endpoints)

A API possui rotas completas para gerenciar o ciclo de vida dos vetores no Pinecone:

- **`POST /buscar`**: Recebe a frase digitada pelo usuário no frontend, gera o embedding e faz a consulta por similaridade de cosseno no Pinecone, retornando os produtos e seus respectivos *scores* de precisão.
- **`POST /upload-produtos`**: Lê o arquivo `produtos.json`, gera os vetores de cada descrição e faz o `upsert` salvando os vetores junto com seus metadados (nome, preço, categoria, descrição) no banco.
- **`DELETE /limpar-banco`**: Executa o reset completo do index do Pinecone para limpeza de dados antigos.

## Como Instalar e Rodar Localmente

1. Certifique-se de ter o **Node.js** instalado na sua máquina.
2. Clone este repositório e acesse a pasta do backend:
```bash
   cd backend
```
3. Instale todas as dependências do projeto:
```bash
  npm install
```
4. Crie um arquivo **`.env`** na raiz do backend e adicione as suas credenciais do Pinecone:
```bash
  PINECONE_API_KEY=sua_chave_secreta_aqui
  PINECONE_INDEX=nome_do_seu_index
```
5. Inicie o servidor:
```bash
  node index
