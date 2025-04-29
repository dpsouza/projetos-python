import pandas as pd

# 1. Carregar o arquivo Excel (substitua pelo seu caminho)
df = pd.read_excel("/content/planilha para estudos.xlsx")

# 2. Função para substituir pontos por vírgulas em uma coluna
def substituir_ponto_por_virgula(coluna):
    return coluna.astype(str).str.replace('.', ',', regex=False)

# 3. Identificar colunas que contêm pontos e aplicar a substituição
for coluna in df.columns:
    # Verifica se há pelo menos um ponto em algum valor da coluna
    # Em regex, o ponto (.) tem um significado especial (representa "qualquer caractere").
    # Usamos \. (com a barra invertida) para "escapar" o ponto e tratá-lo como um caractere literal.
    
    if df[coluna].astype(str).str.contains('\.', regex=True).any():
        df[coluna] = substituir_ponto_por_virgula(df[coluna])

# 4. Mostrar o DataFrame após a limpeza
print("\nDataFrame após substituição de pontos por vírgulas:")
print(df)

# 5. Salvar o resultado (opcional)
df.to_excel("planilha_ajustada.xlsx", index=False)
