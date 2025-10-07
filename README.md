# Tech Challenge 3 - 5IADT
Tech Challenge - Fase 3: Exemplo de Fine-Tuning de um foundation model (Llama, BERT, MISTRAL etc.), utilizando o dataset "The AmazonTitles-1.3MM"
da Pos Tech em IA para Devs da FIAP, 2025, conduzido pelo professor Carlos Aragão

Flavio Luiz Vicco - RM 361664

> Olá, pessoal! Eu sou o Flavio Vicco e hoje vou apresentar o Tech Challenge da Fase 3 da Pos Tech em IA para Devs da FIAP, 2025, conduzido pelo professor Carlos Aragão. Vou mostrar como desenvolvi um pipeline completo de fine-tuning de um modelo de linguagem para gerar resumos automáticos de produtos da Amazon. Vamos entender como o programa funciona, desde o pré-processamento dos dados até o treinamento e avaliação do modelo.

# 🧩 Resumo da lógica de fine-tuning

### 1️⃣ Limpeza e formatação dos dados: transforma o dataset original em pares input → resumo.

### 2️⃣ Geração automática de rótulos (resumos): usa um modelo pré-treinado (BART) para gerar exemplos de saída.

### 3️⃣ Tokenização: converte textos em IDs para o modelo T5.

### 4️⃣ Treinamento (fine-tuning): ajusta o modelo t5-base para aprender a resumir descrições de produtos.

### 5️⃣ Avaliação: mede a qualidade dos resumos com a métrica ROUGE.

### 6️⃣ Validação manual: testa o modelo em exemplos conhecidos e novos.

### 7️⃣ Salvamento e reuso: salva o modelo afinado para uso futuro.
