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
# Необязательные поля, в случае их отсутствия просто передавайте по ключу None:
# 'side_recipient_kpp'
# 'literal_sum'
# 'status'
# 'purpose_code'
# 'uin'
# 'cbc'
# 'okato'
# 'reason'
# 'period'
# 'reason_number'
# 'reason_date'
#  'field_110'
#
payment_order_dict = {
    'creation_date': '21.07.2021',
    'last_transaction_date': '21.07.2021',
    'document_date': '21.07.2021',
    'document_number': '6000',
    'priority': '5',
    'transaction_type_code': '01',
    'purpose': 'Оплата по договору (номер/дата) без НДС',
    'payer_kpp': '773601001',
    'payer_inn': '280267860010',
    'payer_name': 'ООО "БИОШАНЬ"',
    'payer_bank': 'ТОЧКА ПАО БАНКА "ФК ОТКРЫТИЕ"',
    'payer_bank_address': 'г. Москва',
    'side_recipient_inn': '7839443197',
    'side_recipient_bank': 'ПАО Сбербанк',
    'side_recipient_bank_address': 'г. Екатернибург',
    'side_recipient_name': 'АО Точка',
    'side_recipient_kpp': '770501001',
    'transaction_sum': '13636.36',
    'payer_account': '40702810401500014770',
    'payer_bank_code': '044525999',
    'payer_cr_account': '30101810845250000999',
    'side_recipient_bank_code': '044525593',
    'side_recipient_account': '42306810963160914857',
    'side_recipient_cr_account': '30101810845250000999',
    'finance_administrator_name': 'О.С.Берг',
    'literal_sum': 'тысяча рублей 00 копеек',
    'status': '08',
    'purpose_code': '3',
    'uin': '1',
    'cbc': '18210202020061000160',
    'okato': '65401364000',
    'reason': 'ТП',
    'period': 'МС.08.2009',
    'reason_number': '12',
    'reason_date':'10.10.2009',
    'field_110': 'НС',
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