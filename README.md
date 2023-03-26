# payment_order_renderer

Библиотека для создания документов платежного поручения в формате pdf.
Под капотом собрана из библиотеки printpdf для rust.
____
## Установка

> pip install payment-order-renderer

____

## Использование
```python
from payment_order_renderer import create_pdf


# Функция ожидает словарь следующего вида:
# Поля 'side_recipient_kpp' и  'literal_sum' необязательные
# в случае их отсутствия просто передавайте None
payment_order_dict = {
        'creation_date': '2021-07-21T00:00:00+05:00',
        'last_transaction_date': '2021-07-21',
        'document_date': '2021-07-21',
        'document_number': '6000',
        'priority': '5',
        'transaction_type_code': '01',
        'purpose': 'Оплата по договору (номер/дата) без НДС',
        'payer_kpp': '773601001',
        'payer_inn': '280267860010',
        'payer_name': 'ООО "Рога и копыта"',
        'payer_bank': 'БАНК ПЛАТЕЛЬЩИК',
        'payer_bank_address': 'г. Москва',
        'side_recipient_inn': '7839443197',
        'side_recipient_bank': 'ПАО Сбербанк',
        'side_recipient_bank_address': 'г. Екатернибург',
        'side_recipient_name': 'Дядя Толик',
        'side_recipient_kpp': None,
        'transaction_sum': '1488.23',
        'payer_account': '40702810401500014770',
        'payer_bank_code': '044525989',
        'payer_cr_account': '30101810845250000999',
        'side_recipient_bank_code': '044525598',
        'side_recipient_account': '42306810963160914857',
        'side_recipient_cr_account': '30101810845250000999',
        'finance_administrator_name': 'А.В. Прокопчук',
        'literal_sum': 'одна тысяча четыреста восемьдесят рублей 00 копеек',
    }

# Путь до вашего png изображения печати
path = "../pythonProject/pics/stamp_with_signature-1.png"

# Результат возвращается в байтах
result = create_pdf(payment_order_dict, path)
```
+ Внутренняя структура PaymentOrder умеет делать перенос по словам.

+ Суммы вида "6000" и "6000.00" будут размещены на документ ввиде "6000=". Если имеются остатки к примеру "6000.23", то сумма будет размещена в виде "6000-23".
  
+ На данный момент библиотека умеет загружать лишь файлы формата png.
  
+ Для написания текстов используются облегченные шрифты Arial и Arial Bold.

+ Примерный вес получаемого документа ~411 кб, планируется и дальше не выходить за границу 500кб.

____
## TODO
1. Добавить тесты
2. Добавить больше обработок ошибок
3. (Возможно)Сделать печать опциональным параметром