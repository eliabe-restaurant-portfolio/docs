# **Endpoint: `POST /api/auth/reset`**

Inicia o fluxo de redefinição de senha para um usuário. O usuário é inativado nesta operação. Caso o usuário possua outras requisições de reset de senha, elas serão deletadas e será criado um novo reset. As informações do código de confirmação e token de identificação do reset de senha são enviados por email.

## **Requisição**

  * **Método:** `POST`

  * **URL:** `/api/auth/reset`

  * **Headers:**

      * `Content-Type: application/json`

  * **Corpo da Requisição (Body):**

    **Exemplo:**

    ```json
    {
       "email": "email@gmail.com"
    }
    ```

-----

## **Respostas**

### **`200 OK` - Sucesso**

  * **Corpo (Body):**
    ```json
    {
        "success": true,
        "message": "reset password successufully",
        "data": null,
        "code": 200,
        "errors": null
    }
    ```

### **`400 Bad Request` - Usuário não encontrado**

  * **Corpo (Body):**

    ```json
    {
        "success": false,
        "message": "user not found.",
        "data": null,
        "code": 400,
        "errors": ["user not found."]
    }
    ```