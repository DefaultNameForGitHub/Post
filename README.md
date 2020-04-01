        Программа для проверки коммутации приемного устройства.
(Задача: последовательно опросить каждый из 132 МШУ и скоммутировать его в 16 каналов АЦП (далее блок 4201 ЦОС НД и 4201 ЦОС ВД, в каждом 8  кассет АЦП). Сравнить полученный порядковый номер кассеты АЦП с эталонным значением соглано Приложению В Протокола "РПУ Т2/18/40").  

Для решения данной задачи разработан Технологический режим (прокотол БЦОС ВД и БЦОС НД с БИПМ PV-4203).
Он заключается в измерении блоками ЦОС (2 блока, в каждом 8  кассет ЦОС) уровня шумов последовательно переключаемых 132 шт. МШУ   на установленной частоте приема (Во всех состояниях коммутации МШУ согласно  Приложению В Протокола "РПУ Т2/18/40"). Т.о. последовательно перебираются 240 состояний приемного устройства (2 состояния * 132 МШУ - 24 = 240 (24 состояния не используются)). 150 состояний нижнего диапазона (30 для Д2, 30 для Д3, 90 для Д4) коммутируются в 8 кассет блока 4201 НД ЦОС, 90 состояний верхнего диапазона (Д5) коммутируются в 8 кассет блока 4201 ВД ЦОС  Результатом измерений будут уровни шумов в каждой кассете блоков ЦОС на одной, установленной для каждого диапазона, частоте приема для каждого из 240 состояний приемного устройства (8 кассет * 240 состояний = 1920 байт) 

При входе в технологический режим предполагается, что блок ЦОС предварительно переведен в режим паузы командой 0х80, а затем РПУ переведен в Режим тестирования и настроен на требуемую частоту приема и прочие параметры, при помощи отладочного пакета управления РПУ 0х8А.

Далее необходимо последовательно обратиться к каждому из диапазонов приемного устройства с помощи отладочного пакета управления РПУ 0х8А. Ответ будет содержать массив состоящий из n (кол-во состояний в диапазоне) массивов, которые в свою очеречь содержат 8 амплитуд (от каждой кассеты блока ЦОС). Состояния коммутации МШУ перебираются в порядке, соответствующем порядку состояний установленного диапазона частот соглано Приложению В Протокола "РПУ Т2/18/40". Необходимо определить позиционный номер кассеты, в которой амплитуда максимальна и сравнить его с эталонным значением соглано Приложению В Протокола "РПУ Т2/18/40", на основании данного сравнения сделать вывод о правильности физического подключения МШУ к блоку ЦОС.

# Post
        # Пинг интерфейсных плат
        if PING == True:
            # Цикл опроса диапазонов 
            bands = ['D2', 'D3', 'D4', 'D5']
            for band in bands:
            
                if band == 'D2':
                # Настройка на требуемую частоту приема Д2 , при помощи отладочного пакета управления РПУ 0х8А
                elif band == 'D3':             
                elif band == 'D4':
                elif band == 'D5':
                else:
                    pass

                while True:
                    # прием ответа на запрос команды 0х8А                  
                    # проверка посылки на длительность
                    if len(data) == 488:
                    # Д2 и Д3 длина посылки 242 байта (первые 2 байта служебные)
                    elif len(data) == 1448:  
                    # Д2 и Д3 длина посылки 722 байта (первые 2 байта служебные)
                    else:
                        continue                 
                    # деление посылки на отрезки по 8 каналов
                    data = [data[i:i + 8] for i in range(0, len(data), 8)]

                    # поиск максимальной амплитуды в кассетах ЦОС
                    max_lst = [i.index(max(i)) + 1 for i in data]
                    # поиск совпадений с эталонным массивом (задается ранее, здесь не указан)
                    if band == 'D2':
                    # Для каждого диапазона свой эталон
                    elif band == 'D3':
                    elif band == 'D4':
                    elif band == 'D5':
                    else:
                        continue
                    
                    # В массиве comparison содержиться информация о каждом МШУ текущего диапазона (здесь подкрашивается ячейка)
                    for i in comparison:                      
                        if band == 'D2':                         
                        elif band == 'D3':                            
                        elif band == 'D4':                            
                        elif band == 'D5':                            
                        else:
                            pass
                    break
        else:
            print('Not connection')
