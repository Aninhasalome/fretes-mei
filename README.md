# Sistema de Fretes + App Motorista — Marco Tulio Salome Oliveira MEI

---

## PASSO 1 — Criar projeto no Firebase (gratuito)

1. Acesse **console.firebase.google.com** e faça login com conta Google
2. Clique em **"Adicionar projeto"**
3. Nome do projeto: `fretes-marco` → clique em **Continuar**
4. Desative o Google Analytics → **Criar projeto**
5. Aguarde criar e clique em **Continuar**

---

## PASSO 2 — Criar banco de dados Firestore

1. No menu lateral esquerdo clique em **Firestore Database**
2. Clique em **Criar banco de dados**
3. Selecione **Modo de produção** → **Avançar**
4. Selecione local: **southamerica-east1 (São Paulo)** → **Criar**
5. Aguarde criar

---

## PASSO 3 — Configurar regras de segurança

1. No Firestore, clique na aba **Regras**
2. Substitua o conteúdo por:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /fretes_motoristas/{document} {
      allow read, write: if true;
    }
  }
}
```

3. Clique em **Publicar**

---

## PASSO 4 — Pegar as credenciais do Firebase

1. No menu lateral clique em **Configurações do projeto** (engrenagem ⚙)
2. Role até **Seus apps** → clique no ícone **</>** (Web)
3. Nome do app: `fretes-web` → clique **Registrar app**
4. Copie o bloco `firebaseConfig` que aparece — vai ser assim:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "fretes-marco.firebaseapp.com",
  projectId: "fretes-marco",
  storageBucket: "fretes-marco.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

---

## PASSO 5 — Colar as credenciais nos arquivos

### Em index.html (sistema do admin):
Abra o arquivo e procure o bloco:
```javascript
const FIREBASE_CONFIG = {
  apiKey: "COLE_AQUI_SUA_API_KEY",
  ...
```
Substitua cada campo com os valores copiados no Passo 4.

### Em motorista.html (app do motorista):
Faça o mesmo — procure `const FIREBASE_CONFIG` e substitua.

### Em motorista.html — configure os nomes dos motoristas:
Procure:
```javascript
const MOTORISTAS = [
  'Motorista 1',
  'Motorista 2',
  ...
```
Substitua pelos nomes reais dos seus motoristas.

---

## PASSO 6 — Publicar no GitHub Pages

1. Crie conta grátis em **github.com**
2. Crie repositório chamado **fretes-mei** (Public)
3. Faça upload de TODOS os arquivos:
   - index.html
   - motorista.html
   - manifest.json
   - manifest-motorista.json
   - sw.js
   - README.md
   - pasta icons/ (com os 2 arquivos PNG)
4. Vá em **Settings → Pages → Branch: main → Save**
5. Aguarde ~1 minuto

---

## Endereços após publicação

| App | Link |
|-----|------|
| Sistema admin (você) | `https://SEU_USUARIO.github.io/fretes-mei/` |
| App do motorista | `https://SEU_USUARIO.github.io/fretes-mei/motorista.html` |

Envie o link do motorista para cada motorista pelo WhatsApp.

---

## Como o motorista instala no celular (Android)

1. Abra o link do motorista no **Chrome**
2. Toque nos 3 pontinhos → **Adicionar à tela inicial**
3. Confirme — aparece como app na tela inicial

---

## Fluxo de trabalho

```
Motorista registra frete (app)
        ↓ (tempo real)
Admin vê na aba "Motoristas"
        ↓ (clica Aprovar)
Frete lançado automaticamente no sistema
        ↓
Admin completa: tomador, vencimento, emite NF/boleto
```

---

*Marco Tulio Salome Oliveira — CNPJ 53.651.463/0001-80 — Itaúna/MG*
