# 1718-G10
Grupo 10

1) Questões da Parte1 da Aula

1.1 Foram gerados 1024 bytes pseudo aleatórios

34ZVjddAJQUv+HMqfjBPuN+f+viTqpLCeR2FnRp1S+vXewe0/Vcaf7+FVKeRMep7
k/pW8KHUrmmaEjcZY7ByJD4kIRBzBxzE2e/52MmWDDsk9bfPPAtIXRumsuqV/urw
WmfvIt2crSJQrOm8oXeTknHuk/tXz7b9PmmAPkhoojG9NxGS0dpNjG3RL0yydmCR
sKmXGeELtPM3ks3x1hUp728DV3uKUl13bDPBTdHFgukQcZtOpb9gdE+2DEA2Hhp2
skwH+yUZ3PfvcqKVagX/oF0ervpSbIDodzrUwTQd0yklMVSYrQtqrccbw6FEDZCz
A6J/8sDxKaRPOACEulpyJKT1tc2QyjVxjuZlkw8Vq45CqiRR1jtuYF+SDnQXiuSt
DZb6m1GQDrTiNthysXrNzZZuisolsuUIfKWnUK6XUerNXdHOolS9iOJ1hJ/CQpe8
HUNfyo/+fIdtLUmylkisWqUoy++Ew3o5FgPP13uBvI8YA4K7eNHdgNU6eyYBzTEO
eHjK6couuOCRU9xpwfJcXM5rbevyp+PpHzSE1hc+xuQdm7cwo/Hjsy5lVgworhE2
GtqZeqP5gsH8uRcv7UePM4Dbarn8iiVtyXkE9ShtRlLHiVaNcCbl0v+2I85/j1Ix
ecDVXBiO8Fjv0vwIxvxxh0PV1wnagSF+B6fIs6G/kTQd5cw6+gue1fqdDlejcOft
+MyJiLkzdOagKDx39GjJB1PYQsbOXwwmEUvReKYl8WpIaLA2/0xAP7pkhC1CfXGi
9FaTkbwJbIyDIvk+imqPPW9ELaqH8ABGv5PuzPBHBQWAiwlI1VtLxzBKcLxwg+ow
NJQiz3wf9fHOo6y2BZ3NcBp3v/X+rEePFxNqyot0munmIXjomz3w7jy/6vqFBawE
uvF4ETbfo0nc7ENgvqvLUv1a2SmOTcVDw3wpsJp5VZDFMQu9ndtsHjKwBGMkcvEQ
dwCld2+zdOGIKiEc9U4ijdSNqGtpMBzdvLZcDtJ5HuSkAj/FaoreCD9BBMDIO4XP
QlGp5ahCv/QWs9ycNHLx9nylgEBn8PYjkNWOOmGG8XG3Wz5qtwrslQMD/uL0FfCb
YBJwQe+DmFaecv3xkvXQS974PzF/X5J8FWcaoVoAC1GjFrwpt6tHNI/dWU73cOwc
HE0X+Oo+9hlg5ieapiysRBKtrziENZtsXgcTHIZO0Hma8RpGG0wrYgFX5Vn6i3kt
Tz2Hsdvfal+2PdDTGl8uvrVvSoXSvARze4nENoQobPTcCHePwFyBR+7YkHpmODzw
tvrANbTrFV57+c05v9nDeHm2cHaednWgavjOpEWYaIs4FOyGh9GPHcSI+s2FboCi
Q8ah84RFPsKCoZT8pISD3A==

P1.1

Na execução do primeiro comando, para 1024 butes, não foi gerado nenhum byte, porque a máquina precisa de muita entropia.mas se reduzirmos para 24 ou 40 bytes serão gerados os bytes pseudoaleatórios, visto que neste caso a máquina não precisa de entropia.
  No segundo foram gerados os 1024 bytes pseudoaleatórios, pelo facto de introduzir urandom, os bytes pseudoaleatórios são gerados sem precisar de entropia. 
Nos baseamos nos resultados obtidos após a execução dps respectivos comandos.

P1.2

O primeiro comando permitiu gerar 1024 bytes pseudoaleatórios sem presisar da entropia por causa da intalação da package haveged, que é um gerador de bytes pseudoaleatórios.
Para chegar à estas conclusões baseamo-nos nos resultados obtidos durante a execução dos comandos após a instalação da package haveged.
















3) Questões da Parte3 da Aula

P.3

Daria as seguintes sugestões:
1- Usar a cifra simetrica salsa 20 para cifrar o segredo
2- Gerar chaves aleatóriamente com tamanhos maior 2⁸⁰ para garintir maior segurança(no nosso caso usamos 256 bits como experiência)
3- Gerar um mac da mensagem cifrada que sera enviada em conjunto, para garantir autenticidade.
4- Para decifrar, oreceptor recebe o criptograma juntamente com o mac correspondente, calcula o mac da mensagem e compara com o recebido. Se ambos forem iguais, o segredo é autêntico e se não forem iguais implica dizer que o segredo foi vitima de ataque. Deve-se rejeitar a mensangem recebida.

O algoritmo para resolver o referido problema é:

{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 85,
   "metadata": {},
   "outputs": [],
   "source": [
    "# decifar uma mensagem\n",
    "from Crypto.Cipher import Salsa20\n",
    "from cryptography.hazmat.backends import default_backend\n",
    "\n",
    "\n",
    "def cifra(k, txt):\n",
    "    \"\"\" Função que cifra a mensagem 'txt' usando a chave 'k'\"\"\"\n",
    "    cipher = Salsa20.new(key=k)\n",
    "    return cipher.nonce + cipher.encrypt(txt)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 86,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "b'\\xb4\\xfe\\r\\xaaF\\xe2\\xe0jB\\xe2\\xc0\\x7f{\\x86\\x9a\\xd2\\x03nb\\xf3\\x90\\x88P'\n"
     ]
    }
   ],
   "source": [
    "# testar a função 'cifra'\n",
    "secret = b'*Thirty-two byte (256 bits) key*'\n",
    "ctxt = cifra(secret, b'Uma mensagem...')\n",
    "print(ctxt)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 87,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "b'arquivo da impresa' HASH= b'Y+\\x98\\xc4\\xc32C\\x036\\x06\\xfb\\x07V\\xcd\\xea\\x9dfj\\x87\\x85\\x07\\xf3\\x01\\xb0\\x81\\xe6\\xa9\\xef<\\x1d\\x9d\\xd6'\n"
     ]
    }
   ],
   "source": [
    "from Crypto.Cipher import Salsa20\n",
    "\n",
    "msg_nonce = msg[:8]\n",
    "ciphertext = msg[8:]\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "secret = b'*Thirty-two byte (256 bits) key*'\n",
    "cipher = Salsa20.new(key=secret, nonce=msg_nonce)\n",
    "digest = hashes.Hash(hashes.SHA256(), backend=default_backend())\n",
    "plaintext = cipher.decrypt(ciphertext)\n",
    "digest.update(plaintext)\n",
    "h = digest.finalize()\n",
    "\n",
    "print(plaintext, \"HASH=\", h)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 88,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "32\n"
     ]
    }
   ],
   "source": [
    "from cryptography.hazmat.primitives import hashes\n",
    "\n",
    "digest = hashes.Hash(hashes.SHA256(), backend=default_backend())\n",
    "digest.update(b\"abc\")\n",
    "digest.update(b\"123\")\n",
    "res = digest.finalize()\n",
    "print(len(res))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 89,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "b'\\xdbP\\xa2*\\xe4q^\\xcb\\xa51}\\xa2Z\\x81]\\x86\\xcb\\xa2\\xfbP\\x95\\t6E3V,i\\xfb\\xc40f'"
      ]
     },
     "execution_count": 89,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from cryptography.hazmat.primitives import hashes, hmac\n",
    "h = hmac.HMAC(secret, hashes.SHA256(), backend=default_backend())\n",
    "h.update(b\"message to hash\")\n",
    "h.finalize()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
