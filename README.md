openapi: 3.0.0
info: 
  version: 1.0.0
  title: Бронирование мест в киотетр "Искорка"
  description:  Домашнее задание Swagger 
paths:
  /sessions:
    get:
      parameters:
        - name: Film
          desctiption: Название фильма
          in: query
          schema:
            type: string
            example: "Револьвер"
        - name: description
          description: описание фильма
          in: query
          schema:
            type: string
            example: "Криминальный боевик"
        - name: seat_available
          description: свободные места
          in: query
          schema:
            type: array
            example: ряд 7 место 7
        - name: Price
          description: цена билета
          in: query
          schema:
            type: decimal
            example: 550
        - name: Date_Session
          description: дата и время сеанса
          in: query
          schema:
            type: string
            format: date-time
            example: 29.04.2025 16:00
      responses:
      200:
        description: ok
        content:
          application/json:
            schema:
            type: array
            items:
              type: object
              propertis:
                SessionID:
                  type: integer
                  description: идентификатор сеанса фильма
                  example: 123
                Film:
                  type: string
                  description: название фильма в сеансе
                  example: фильм "Револьвер"
                Description:
                  type: string
                  description: Жанр фильма
                  example: Криминальный боевик
                Seat_available: 
                  type: array
                  desctiption: свободные места на сеанс
                  items:
                    type: string
                  example: 
                    - ряд 7 место 7
                    - ряд 7 место 8
                  Price:
                    type: decimal
                    description: цена билета
                    example: 550
                  Date_session:
                    type: string
                    format: date-time
                    description: дата и время сеанса
                    example: 29.04.2025 16:00
  /orders: 
    post:
      summary: Создать новый заказ на билет
      description: Забронировать место в зале для выбранного фильма и сеанса.
      parameters:
        - name: Seat_available
          in: path
          required: true
          description: Место в зале, которое нужно забронировать 
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                Film:
                  type: string
                  description: Название фильма
                  example: Револьвер
                Date_Session:
                  type: string
                  description: Дата и время сеанса 
                  example: 29.04.2025 16:00
                Seat_available:
                  type: string
                  description: Место в зале
                  example: 
                    - ряд 7 место 7
                    - ряд 7 место 8
      responses:
        200:
          description: Успешное создание заказа
          content:
            application/json:
              schema:
                type: object
                properties:
                  OrderID:
                    type: string
                    description: Уникальный идентификатор заказа
                    example: 123
                  Film:
                    type: string
                    description: Название фильма
                    example: Револьвер
                  Date_Session:
                    type: string
                    description: Дата и время сеанса
                    example: 29.04.2025 16:00
                  Seat_available:
                    type: array
                    items:
                      type: string
                    description: Место в зале
                    example:
                      - "ряд 7 место 7"
                  Phone:
                    type: string
                    description: Номер телефона покупателя
                    example: "+7-999-123-45-67"
                  Price:
                    type: decimal
                    description: Цена билета
                    example: 550
  delete:
      summary: Удаление заказа
      description: Запрос на удаление заказа
      tags: 
        - Заказы
      parameters:
        - name: id
          in: path
          required: true
          description: Идентификатор заказа
          schema: 
            type: integer
            example: 123
      responses:
        200: 
          description: заказ удален
          content:
            application/json:
              schema:
                type: array
                items: 
                      type: string
                      example: Заказ успешно удалён
  /Orders/{id}/Seat_available:
    patch:
      summary: Изменение заказа
      description: Изменение заказа
      tags: 
        - Заказы
      parameters:
        - name: id
          in: path
          required: true
          description: Идентификатор заказа
          schema: 
            type: integer
            example: 123
      requestBody:
        content:
          application/json:
            schema:
              properties:
                Seat_available:
                  type: string
                  example: ряд 7 место 8           
      responses:
        200: 
          description: Заказ обновлен
          content:
            application/json:
              schema:
                properties: 
                  errors:
                    type: array
                    items: 
                      type: string
                    example: []
                  result: 
                  OrdersResponse:
      type: object
      properties:
        OrderID:
          type: integer
          description: Идентификатор заказа
          example: 123
        Film:
          type: string
          description: Название фильма
          example: Револьвер
        Date_Session:
          type: string
          format: date-time
          description: Дата и время сеанса
          example: 29.04.2025 16:00
        Seat_available:
          type: integer
          description: Текущее место в зале
          example: ряд 7 место 8
        Phone:
          type: string
          description: Контактный телефон
          example: "+7-999-876-54-32"
        Price:
          type: decimal
          description: Стоимость заказа в рублях
          example: 550
                example: []
                result: 
                    properties:
                      message:
                        type: string
                        example: Заказ успешно удалён
    /Orders/{id}
patch:
      summary: Изменение заказа
      description: Изменение заказа
      tags: 
        - Заказы
      parameters:
        - name: id
          in: path
          required: true
          description: Идентификатор заказа
          schema: 
            type: integer
            example: 123
      requestBody:
        content:
          application/json:
            schema:
              properties:
                Seat_available:
                  type: string
                  Seat_available:
                  type: string
                  example: ряд 7 место 8
      responses:
        200: 
          description: Заказ обновлен
          content:
            application/json:
              schema:
                properties: 
                  errors:
                    type: array
                    items: 
                      type: string
                    example: []
                  result: 
                  OrdersResponse:
      type: object
      properties:
        OrderID:
          type: integer
          description: Идентификатор заказа
          example: 123
          Film:
          type: string
          description: Название фильма
          example: Револьвер
        Date_Session:
          type: string
          format: date-time
          description: Дата и время сеанса
          example: 29.04.2025 16:00
        Seat_available:
          type: integer
          description: Текущее место в зале
          example: ряд 7 место 8
        Phone:
          type: string
          description: Контактный телефон
          example: "+7-999-876-54-32"
        Price:
          type: decimal
          description: Стоимость заказа в рублях
          example: 550
  
  servers:
    - description: SwaggerHub API Auto Mocking
      url: Https://virtserver.swaggerhub.com
