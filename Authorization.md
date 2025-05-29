# TestRyphie

// АВТОРИЗАЦИЯ (КНОПКА ВХОДА)

hotelEntities db = new hotelEntities(); // hotelEntities - СВОЯ БАЗА
        public MainWindow() 
        { 
            InitializeComponent(); 
        } 
        private void Button1_Click(object sender, RoutedEventArgs e) 
        { 
           
            try 
            { 
                
                var user = (from x in db.Users              // Users -- Таблица из БД
                            where x.login == TextBox1.Text  // login -- название переменной в таблице из БД
                            select x).ToArray(); 
 
                
                if (TextBox1.Text.Length == 0 || TextBox2.Text.Length == 0) 
                { 
                   
                    MessageBox.Show("Поля Логин и Пароль обязательны для заполнения", 
                    "!", MessageBoxButton.OK, MessageBoxImage.Error); 
                } 
                else 
                { 
                    if (TextBox1.Text == user[0].login) 
                    { 
                        if(TextBox2.Text == user[0].password) 
                        { 
                            switch (user[0].role2) 
                            { 
                                case 1: 
                                    MessageBox.Show("Добро пожаловать. Вы успешно 
авторизировались как администратор  " + user[0].surname, "Уведомление", MessageBoxButton.OK, 
MessageBoxImage.Information); 
                                    Window1 window = new Window1(); 
                                    window.Show(); 
                                    break; 
                                case 2: 
                                    MessageBox.Show("Добро пожаловать. Вы успешно 
авторизировались как пользователь  " + user[0].surname, "Уведомление", MessageBoxButton.OK, 
MessageBoxImage.Information); 
                                    Window2 window1 = new Window2(); 
                                    window1.Show(); 
                                    break; 
                                default: 
                                    MessageBox.Show("Данные не обнаружены", "Уведомление", 
MessageBoxButton.OK, MessageBoxImage.Information); 
                                    break; 
                            } 
 
                        } 
                        else  
                        { 
                            MessageBox.Show("Вы ввели неверный логин или пароль", "Пожалуйста 
проверьте ещё раз введенные данные",  
                                MessageBoxButton.OK, MessageBoxImage.Error); 
                        } 
                    } 
                
                } 
 
            } 
 
            catch (SystemException) 
            { 
                MessageBox.Show("Ошибка системы", "Ошибка", MessageBoxButton.OK, 
MessageBoxImage.Error); 
            } 
        }
