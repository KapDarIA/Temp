# Задание 1

int main()
{
	setlocale(0, "ru");
	int a = -15;
	int b = 1234;
	int min;
	_asm {
		mov EAX, a
		mov EBX, b
		CMP EBX, EAX
		JLE min_number1
		mov min, EAX
		JMP end_fun
		min_number1:
			mov min, EBX
		end_fun:
     }
	cout << "Наименьшее число: " << min;
}

# Задание 2

int main()
{
	setlocale(0, "ru");
	int a = -1204;
	int b = 904;
	int c = -1212;
	int max;
	_asm {
		mov EAX, a
		mov EBX, b
		mov EDX, c

		CMP EAX,EBX
		JL CONTINUE1
			mov max,EAX
			JMP CONTINUE2
		CONTINUE1:
		mov max, EBX

		CONTINUE2:
		CMP max, EDX
		JG END
			mov max, EDX
			JMP END
		END:
	}
	cout << "Наибольшее число: " << max;
}

# Задание 3

int main()
{
    int a = 5;
    int x = 3;
    int y;
    _asm {
        mov EAX, a
        mov EBX, x
        CMP EBX, -10
        JL fun1
        CMP EBX, 10
        JGE fun3
        FLD x
        FABS
        FSTP x
        IMUL EAX, x
        MOV y, EAX
        JMP END

        fun1:
            IMUL EBX, x
            IMUL EAX,EBX
            MOV y, EAX
            JMP END
        fun3:
            SUB EAX, EBX
            MOV y,EAX
            JMP END
        END:
    }
    cout << y;
}

# Задание 4

int main()
{
	setlocale(0, "ru");
	int month;
	cin >> month;
	int days;
	_asm {
		mov EAX, month
		CMP EAX, 1
		JE equal31
		CMP EAX, 3
		JE equal31
		CMP EAX, 4
		JE equal30
		CMP EAX, 5
		JE equal31
		CMP EAX, 6
		JE equal30
		CMP EAX, 7
		JE equal31
		CMP EAX, 8
		JE equal31
		CMP EAX, 9
		JE equal30
		CMP EAX, 10
		JE equal31
		CMP EAX, 11
		JE equal30
		CMP EAX, 12
		JE equal31
		mov EDX, 28
		JMP END
		equal30 :
		mov EDX, 30
			JMP END
		equal31:
			mov EDX, 31
			JMP END
		END:
		mov days, EDX
	}
	cout << "Количество дней в месяце: " << days;
}

# Задание 5

int main()
{
    setlocale(0, "ru");
	int sum;
	cin >> sum;
	int cost = 1000;
	_asm {
		mov EAX, sum
		SUB EAX, cost
		mov sum, EAX
	}
	if (sum == 0)
		cout << "Спасибо!";
	else if (sum < 0)
		cout << "Недостаточно: " << -sum;
	else
		cout << "Возьмите сдачу: " << sum;
}
