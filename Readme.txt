from contextlib import contextmanager
import pandas as pd


@contextmanager
def get_test():
    try:
        start_time = pd.Timestamp.now()
        yield
    finally:
        end_time = pd.Timestamp.now()
        time_spent = end_time - start_time
        print(f'Start time: {start_time}\n'
              f'End time: {end_time}\n'
              f'{time_spent.microseconds / 1000000} seconds spent.')


class Test:
    def __init__(self):
        self.start_time = None

    def __enter__(self):
        self.start_time = pd.Timestamp.now()

    def __exit__(self, exc_type, exc_val, exc_tb):
        end_time = pd.Timestamp.now()
        time_spent = end_time - self.start_time
        print(f'Start time: {self.start_time}\n'
              f'End time: {end_time}\n'
              f'{time_spent.microseconds / 1000000} seconds spent.')


n = 10000000
with Test():
    print(f'Сумма первых {n} натуральных чисел равна {sum(range(1,n+1))}')