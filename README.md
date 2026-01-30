flowchart TD
    Start([Начало: Сегодня нужно на работу]) --> CheckCard[Проверить баланс карты]
    CheckCard --> DecisionBalance{Баланс < 500 ₽?}
    
    DecisionBalance -- Да --> TopUpCard[Пополнить карту]
    TopUpCard --> GatherInfo
    DecisionBalance -- Нет --> GatherInfo
    
    GatherInfo[Определить:<br>местоположение, адрес работы,<br>время начала работы] --> EnterApp[Внести данные в Я.Карты]
    EnterApp --> CheckFactors[Проверить:<br>погоду, пробки, отмены транспорта]
    CheckFactors --> ChooseRoute[Выбрать оптимальный маршрут<br>по времени/стоимости/комфорту]
    ChooseRoute --> GoToStop[Пойти к точке посадки]
    
    GoToStop --> WaitTransport[Ожидать транспорт]
    WaitTransport --> ParallelTimeCheck{Транспорт опаздывает?}
    
    ParallelTimeCheck -- Да --> CheckLate{Опаздываю?}
    ParallelTimeCheck -- Нет --> TransportArrived{Транспорт прибыл?}
    
    CheckLate -- Да --> NotifyColleagues[Уведомить коллег об опоздании]
    NotifyColleagues --> TransportArrived
    CheckLate -- Нет --> TransportArrived
    
    TransportArrived -- Нет --> UpdateLocation[Определить текущее<br>местоположение]
    UpdateLocation --> Recalculate[Выбрать оптимальный маршрут]
    Recalculate --> GoToStop
    
    TransportArrived -- Да --> BoardTransport[Сесть на транспорт]
    BoardTransport --> Travel[Выйти на нужной остановке]

    
    Travel --> DecisionTransfer{Это пересадка?}
    
    DecisionTransfer -- Да -->  GoToStop
    DecisionTransfer -- Нет -->  WalkToWork[Дойти до места работы]
    WalkToWork --> End([Я на месте!])
    
    %% Стилизация
    style Start fill:#e1f5e1
    style End fill:#e1f5e1
    style NotifyColleagues fill:#fff3cd
    style CheckLate fill:#ffebee
    style ParallelTimeCheck fill:#fff3cd
