# **Endpoint: `POST /api/auth/login`**

Autentica um usuário no sistema utilizando e-mail e senha. Em caso de sucesso, retorna os dados do usuário e um **token de acesso JWT** que deve ser utilizado para autorizar requisições a endpoints protegidos. O sistema implementa um mecanismo de segurança que bloqueia a conta do usuário após um número excessivo de tentativas de login falhas. Somente usuários ativos podem se logar.

## **Requisição**

  * **Método:** `POST`

  * **URL:** `/api/auth/login`

  * **Headers:**

      * `Content-Type: application/json`

  * **Corpo da Requisição (Body):**

    **Exemplo:**

    ```json
    {
       "email": "email@gmail.com",
       "password": "#SenhaForte1234"
    }
    ```

-----

## **Respostas**

### **`200 OK` - Sucesso**

  * **Corpo (Body) - Login bem-sucedido:**
    ```json
    {
        "success": true,
        "message": "login successfully",
        "data": {
            "user_token": "bcc404ef-93ac-4594-a15d-2df3e01e3596",
            "status": "active",
            "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
            "expires_at": "2025-08-25T16:24:04Z",
            "issued_at": "2025-08-25T15:54:04Z"
        },
        "code": 200,
        "errors": null
    }
    ```

### **`401 Unauthorized` - Usuário Bloqueado**

  * **Corpo (Body) - Usuário Bloqueado:**
    ```json
    {
        "success": true,
        "message": "user has blocked.",
        "data": null,
        "code": 200,
        "errors": null
    }
    ```

### **`401 Unauthorized` - Credenciais Inválidas**

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

### **`401 Unauthorized` - Usuário Inativo**

  * **Corpo (Body) - Usuário Inativo:**
    ```json
    {
        "success": false,
        "message": "user is inactive.",
        "data": null,
        "code": 403,
        "errors": ["user is inactive."]
    }
    ```

### **`404 Not Found` - Usuário Não Encontrado**

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "user not found.",
        "data": null,
        "code": 404,
        "errors": ["user not found."]
    }
    ```