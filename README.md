from datetime import datetime

def calcular_idade():
    print("=" * 40)
    print("       CALCULADORA DE IDADE       ")
    print("=" * 40)
    
    # 1. Captura a data atual do sistema
    hoje = datetime.now()
    
    # 2. Pede e valida os dados digitados pelo usuário
    while True:
        try:
            print("\nDigite os dados do seu nascimento:")
            dia = int(input("👉 Dia (ex: 25): "))
            mes = int(input("👉 Mês (ex: 12): "))
            ano = int(input("👉 Ano (ex: 1995): "))
            
            # Valida se a data existe
            data_nascimento = datetime(ano, mes, dia)
            
            if data_nascimento > hoje:
                print("❌ A data de nascimento não pode ser no futuro! Tente novamente.")
                continue
                
            break 
        except ValueError:
            print("❌ Data inválida! Certifique-se de digitar números corretos (ex: meses de 1 a 12).")

    # 3. Lógica do cálculo precisa de anos, meses e dias
    anos = hoje.year - data_nascimento.year
    meses = hoje.month - data_nascimento.month
    dias = hoje.day - data_nascimento.day

    # Ajusta os dias se o dia atual for menor que o dia de nascimento
    if dias < 0:
        # Pega o mês anterior ao mês atual
        mes_anterior = hoje.month - 1 if hoje.month > 1 else 12
        ano_anterior = hoje.year if hoje.month > 1 else hoje.year - 1
        
        # Descobre quantos dias tinha o mês passado de forma automática e segura
        if mes_anterior == 12:
            proximo_mes = datetime(ano_anterior + 1, 1, 1)
        else:
            proximo_mes = datetime(ano_anterior, mes_anterior + 1, 1)
            
        dias_no_mes = (proximo_mes - datetime(ano_anterior, mes_anterior, 1)).days
        
        dias += dias_no_mes
        meses -= 1

    # Ajusta os meses se o mês atual for menor que o mês de nascimento
    if meses < 0:
        meses += 12
        anos -= 1

    # 4. Exibe o resultado na tela
    print("\n" + "=" * 40)
    print("📊 RESULTADO DA SUA IDADE:")
    print(f"   • {anos} anos")
    print(f"   • {meses} meses")
    print(f"   • {dias} dias")
    print("=" * 40)

if __name__ == "__main__":
    calcular_idade()
