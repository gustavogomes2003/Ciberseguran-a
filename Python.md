import datetime
import os

def coletar_logs():
    caminho_log = "/var/log/auth.log"  # Para sistemas Debian/Ubuntu
    data = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    logs_relevantes = []

    with open(caminho_log, "r") as arquivo:
        linhas = arquivo.readlines()
        for linha in linhas:
            if "Failed password" in linha or "authentication failure" in linha:
                logs_relevantes.append(f"{data},{linha.strip()}")

    with open("logs_suspeitos.csv", "a") as saida:
        for log in logs_relevantes:
            saida.write(log + "\n")

if __name__ == "__main__":
    coletar_logs()
