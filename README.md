public class Calculator {
    public static double divide(double numerator, double denominator) {
        if (denominator == 0) {
            Log.e("Calculator", "Ошибка: деление на ноль.");
            throw new ArithmeticException("Деление на ноль недопустимо.");
        }
        return numerator / denominator;
    }
}

#...

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        try {
            double result = Calculator.divide(10, 0); // Здесь будет вызвана ошибка
            Log.i("MainActivity", "Результат: " + result);
        } catch (ArithmeticException e) {
            Log.e("MainActivity", "Ошибка при делении: " + e.getMessage());
        }
    }
}

#...

import static org.junit.Assert.*;
import org.junit.Test;

public class ExampleUnitTest {
    @Test
    public void testDividePositive() {
        double result = Calculator.divide(10, 2);
        assertEquals(5, result, 0);
    }

    @Test(expected = ArithmeticException.class)
    public void testDivideByZero() {
        Calculator.divide(10, 0);
    }
}

#...

@Composable
fun LoginScreen() {
    var username by remember { mutableStateOf("") }
    var password by remember { mutableStateOf("") }
    var message by remember { mutableStateOf("") }

    Column {
        TextField(
            value = username,
            onValueChange = { username = it },
            label = { Text("Логин") },
            modifier = Modifier.testTag("usernameField")
        )
        TextField(
            value = password,
            onValueChange = { password = it },
            label = { Text("Пароль") },
            modifier = Modifier.testTag("passwordField")
        )
        Button(onClick = {
            if (username == "user" && password == "password") {
                message = "Успешная авторизация"
            } else {
                message = "Неверные учетные данные"
            }
        }) {
            Text("Вход")
        }
        Text(text = message, modifier = Modifier.testTag("messageLabel"))
    }
}

#...

@get:Rule
var composeTestRule = createComposeRule()

@Test
fun testSuccessfulLogin() {
    composeTestRule.setContent {
        LoginScreen()
    }

    composeTestRule.onNodeWithTag("usernameField").performTextInput("user")
    composeTestRule.onNodeWithTag("passwordField").performTextInput("password")
    composeTestRule.onNodeWithText("Вход").performClick()
    composeTestRule.onNodeWithTag("messageLabel").assertTextEquals("Успешная авторизация")
}

@Test
fun testFailedLogin() {
    composeTestRule.setContent {
        LoginScreen()
    }

    composeTestRule.onNodeWithTag("usernameField").performTextInput("user")

    composeTestRule.onNodeWithTag("passwordField").performTextInput("wrongpassword")
    composeTestRule.onNodeWithText("Вход").performClick()
    composeTestRule.onNodeWithTag("messageLabel").assertTextEquals("Неверные учетные данные")
}

