flowchart TD
    Start([Начало: Сегодня нужно на работу]) --> CheckCard[Проверить проездной/баланс карты]
    CheckCard --> DecisionBalance{Баланс < 200 ₽?}
    
    DecisionBalance -- Да --> TopUpCard[Пополнить карту]
    TopUpCard --> GatherInfo
    DecisionBalance -- Нет --> GatherInfo
    
    GatherInfo[Определить:<br>местоположение, адрес работы,<br>время начала работы] --> EnterApp[Внести данные в Яндекс.Карты]
    EnterApp --> CheckFactors[Проверить:<br>погоду, пробки, отмены транспорта]
    CheckFactors --> ChooseRoute[Выбрать оптимальный маршрут<br>по времени/деньгам/комфорту]
    ChooseRoute --> GoToStop[Пойти к точке посадки]
    
    GoToStop --> WaitTransport[Ожидать транспорт]
    WaitTransport --> ParallelTimeCheck{Время ожидания > 15 мин?}
    
    ParallelTimeCheck -- Да --> CheckLate{Опаздываю?}
    ParallelTimeCheck -- Нет --> TransportArrived{Транспорт прибыл?}
    
    CheckLate -- Да --> NotifyColleagues[Уведомить коллег об опоздании]
    NotifyColleagues --> TransportArrived
    CheckLate -- Нет --> TransportArrived
    
    TransportArrived -- Нет --> UpdateLocation[Определить текущее<br>местоположение]
    UpdateLocation --> Recalculate[Пересчитать маршрут]
    Recalculate --> GoToStop
    
    TransportArrived -- Да --> BoardTransport[Сесть на транспорт]
    BoardTransport --> Travel[Ехать до нужной остановки]
    
    Travel --> DecisionTransfer{Это пересадка?}
    
    DecisionTransfer -- Да --> GoToStop
    DecisionTransfer -- Нет --> ExitTransport[Выйти на остановке]
    ExitTransport --> WalkToWork[Дойти до места работы]
    WalkToWork --> End([Я на месте!])
    
    %% Стилизация
    style Start fill:#e1f5e1
    style End fill:#e1f5e1
    style NotifyColleagues fill:#fff3cd
    style CheckLate fill:#ffebee
    style ParallelTimeCheck fill:#fff3cd
