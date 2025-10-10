# Tech Challenge 3 - 5IADT
Tech Challenge - Fase 3: Exemplo de Fine-Tuning de um foundation model (Llama, BERT, MISTRAL etc.), utilizando o dataset "The AmazonTitles-1.3MM"
da Pos Tech em IA para Devs da FIAP, 2025, conduzido pelo professor Carlos Aragão

Flavio Luiz Vicco - RM 361664

https://youtu.be/RQl69dSBtao

> Olá, pessoal! Eu sou o Flavio Vicco e hoje vou apresentar o Tech Challenge da Fase 3 da Pos Tech em IA para Devs da FIAP, 2025, conduzido pelo professor Carlos Aragão. Vou mostrar como desenvolvi um pipeline completo de fine-tuning de um modelo de linguagem para gerar resumos automáticos de produtos da Amazon. Vamos entender como o programa funciona, desde o pré-processamento dos dados até o treinamento e avaliação do modelo.

# ⚙️ Resumo da lógica de fine-tuning

### 📦 1️⃣ Carregamento, limpeza e formatação dos dados: transforma o dataset original em pares input → resumo.
A primeira etapa é a base de tudo: preparar os dados.
O programa lê um arquivo JSON contendo descrições de produtos.
Para otimizar o uso de memória, ele limita a leitura aos cem mil primeiros registros.
Depois, o código cria um DataFrame com apenas as colunas importantes: o título e a descrição do produto.
Linhas vazias ou duplicadas são removidas, garantindo que o modelo aprenda apenas com informações relevantes.

<img width="234" height="131" alt="image" src="https://github.com/user-attachments/assets/53aa07e4-54b2-4bba-8c07-071c5d5b812a" />

### ✏️ 2️⃣ Exportar o Dataset limpo
Com o conjunto de dados limpo, o próximo passo é salvar tudo em formato JSONL —
um formato onde cada linha é um registro independente.
Isso facilita o processamento de grandes volumes e é o padrão usado em treinamento nos modelos na OpenAI e Hugging Face.

<img width="256" height="26" alt="image" src="https://github.com/user-attachments/assets/b411e27d-cc30-4145-8d9d-4d747d2f2b93" />

### 🤖 3️⃣ Geração de resumos automáticos com BART para gerar exemplos de saída.
Agora começa a parte interessante!
Antes de treinar o modelo, precisamos de exemplos de entrada e saída — ou seja, textos e seus resumos.
Aqui usamos o modelo facebook/bart-large-cnn, um modelo pré-treinado da Hugging Face, para gerar automaticamente os resumos iniciais.
A função grava os resultados incrementalmente, economizando memória

### 🧠 4️⃣ Preparação do dataset para fine-tuning
Com os resumos prontos, criamos o dataset final para o fine-tuning.
O programa lê o arquivo de resumos e monta pares input → output,
onde o input contém o título e a descrição, e o output é o resumo gerado.
O texto começa com o prefixo ‘summarize:’, que ajuda o modelo T5 a entender a tarefa.

### 🔤 5️⃣ Tokenização: converte textos em IDs para o modelo T5.
A próxima etapa é converter os textos em tokens.
Usamos o tokenizer do modelo T5-base, limitando o tamanho máximo de entrada e saída.
Isso prepara o dataset para ser processado pela rede neural

### 🧩 6️⃣ Treinamento (fine-tuning): ajusta o modelo t5-base para aprender a resumir descrições de produtos.
Aqui acontece o fine-tuning de verdade!
O modelo T5-base é carregado e treinado com nossos dados.
Definimos hiperparâmetros como número de épocas, tamanho do batch e diretório de logs.
Usamos a métrica ROUGE, que mede a similaridade entre o resumo gerado e o real.

<img width="904" height="153" alt="image" src="https://github.com/user-attachments/assets/4935d5ca-6b44-4ec0-9420-c4a0f86efe54" />

### 🧪 7️⃣ Avaliação: mede a qualidade dos resumos com a métrica ROUGE.
Após o treinamento, testamos o modelo com exemplos reais.
O código gera novos resumos e imprime o resultado decodificado.
Primeiro testamos manualmente alguns produtos.
Depois, avaliamos automaticamente usando o ROUGE — que nos dá um valor numérico da qualidade do resumo

<img width="1810" height="476" alt="image" src="https://github.com/user-attachments/assets/568756eb-8eba-4ff6-913b-f4f41052d741" />

### 💾 8️⃣ Salvamento e reuso: salva o modelo afinado para uso futuro.
Por fim, o modelo é salvo e recarregado para validação.
Primeiro testamos manualmente alguns produtos.
Depois, avaliamos automaticamente usando o ROUGE — que nos dá um valor numérico da qualidade do resumo.
