# **Endpoint: `POST /api/auth/change`**

Permite que um **usuário autenticado** altere sua própria senha. O usuário deve fornecer sua senha antiga para verificação e a nova senha desejada. O sistema rastreia tentativas falhas, e múltiplas tentativas com a senha antiga incorreta podem levar ao bloqueio da conta por segurança.

## **Requisição**

  * **Método:** `POST`

  * **URL:** `/api/auth/change`

  * **Headers:**

      * `Content-Type: application/json`
      * `Authorization: Bearer <seu-jwt-token>`

  * **Corpo da Requisição (Body):**

    **Exemplo:**

    ```json
    {
       "new_password": "#SenhaForteNova1",
       "old_password": "#SenhaForteAntiga123"
    }
    ```

-----

## **Respostas**

### **`200 OK` - Sucesso**

  * **Corpo (Body) - Senha Alterada:**
    ```json
    {
        "success": true,
        "message": "password change successfully",
        "data": null,
        "code": 200,
        "errors": null
    }
    ```

### **`401 Unauthorized` - Credenciais Inválidas**

Retornado se o usuário que está tentando alterar a senha está com o status "inativo".

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "block user.",
        "data": null,
        "code": 401,
        "errors": ["block user"]
    }
    ```

### **`401 Unauthorized` - Credenciais Inválidas**

Retornado quando a `old_password` fornecida está incorreta. A mensagem de erro informa o número de tentativas falhas.

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "invalid credentials. failed attempt: 1",
        "data": null,
        "code": 401,
        "errors": ["invalid credentials. failed attempt: 1"]
    }
    ```