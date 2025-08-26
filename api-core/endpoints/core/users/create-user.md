# **Endpoint: `POST /api/users`**

Cria um novo usuário no sistema. O usuário é criado com status "INATIVO", sendo necessário usar o endpoint de ativação de usuário. É verificado se já existe algum usuário com mesmo email ou CPF no sistema, caso exista, o usuário não é criado. Caso o usuário seja criado, um email é enviado o usuário com o código de ativação que dura 30 minutos e o token que identifica o recurso de mudança de senha no banco de dados. A senha é armazenada no banco encriptada também.

O código de ativação é encriptado no banco a fim de que somente o usuário que recebeu o email tenha ciência do valor do código.

## **Requisição**

  * **Método:** `POST`

  * **URL:** `/api/users`

  * **Headers:**

      * `Content-Type: application/json`

  * **Corpo da Requisição (Body):**

      * É necessário enviar os dados do usuário a ser criado: nome, email e documento de identificação CPF.

    **Exemplo:**

    ```json
    {
      "username": "John Doe",
      "email": "johndoe@example.com",
      "tax_number": "123456789"
    }
    ```

## **Respostas**

### **`200 OK` - Sucesso**

Retornado quando o usuário é criado com sucesso.

  * **Corpo (Body):**
    ```json
    {
        "success": true,
        "message": "user created",
        "data": {
            "UserToken": "b4c0720f-fb17-459e-8ba0-bc8f6647a9b4",
            "Status": "inactive"
        },
        "code": 200,
        "errors": null
    }
    ```

#### **`400 Bad Request` - Usuário Repetido**

Retornado se um usuário com o mesmo e-mail ou cpf já existir no sistema.

  * **Corpo (Body):**
    ```json
    {
        "success": false,
        "message": "repeated user",
        "data": null,
        "code": 400,
        "errors": ["repeated user"]
    }
    ```