# Tech Challenge3 - 5IADT
Tech Challenge - Fase 3: Exemplo de Fine-Tunining de um foundation model (Llama, BERT, MISTRAL etc.), utilizando o dataset "The AmazonTitles-1.3MM"
da Pos Tech em IA para Devs da FIAP, 2025, conduzido pelo professor Carlos Aragão

Flavio Luiz Vicco - RM 361664

🧩 Resumo da lógica de fine-tuning

Limpeza e formatação dos dados: transforma o dataset original em pares input → resumo.

Geração automática de rótulos (resumos): usa um modelo pré-treinado (BART) para gerar exemplos de saída.

Tokenização: converte textos em IDs para o modelo T5.

Treinamento (fine-tuning): ajusta o modelo t5-base para aprender a resumir descrições de produtos.

Avaliação: mede a qualidade dos resumos com a métrica ROUGE.

Validação manual: testa o modelo em exemplos conhecidos e novos.

Salvamento e reuso: salva o modelo afinado para uso futuro.
