# 입력 파일이 여러개인 경우

입력 파일이 여러개인 경우는 1개인 경우 예제에서 ```getopt()``` 함수에 입력 받고자 하는 옵션을 추가하고,  ```switch``` 문에서 추가한 옵션에 대한 코드를 추가하면 됩니다.

예를들어 ```-i, -m``` 옵션 2개를 통해 입력 파일을 받기 원한다면, ```“i:” -> “i:m:”```으로 고치고, 아래 ```switch```문의 ```m``` case를 추가하면 됩니다.


```c
#include <stdio.h>
#include <stdlib.h>
#include <getopt.h>

int main (int argc, char *argv[]) {
	int opt;
	FILE *fp_input;
	FILE *fp_mesh;         //mesh 파일을 읽기 위한 파일 포인터 추가 선언
...

...
	// Detect the end of the options.
	while((opt = getopt(argc, argv, "i:m:")) != -1 ) {
		switch(opt) {
			case 'i':
				if((fp_input = fopen(optarg,"r")) == NULL ) {
					fprintf(stderr, "Error opening inputfile Path: %s\n", optarg);
					return -1;
				} else {
					printf("Succeed to open inputfile Path: %s\n", optarg);
				}
				break;
    			case 'm':
    				if((fp_mesh = fopen(optarg,"r")) == NULL ) {
    					fprintf(stderr, "Error opening meshfile Path: %s\n", optarg);
    					return -1;
    				} else {
    					printf("Succeed to open meshfile Path: %s\n", optarg);
    				}
    				break;
			default:
				printf("Usage: %s -i [inputfile] -m [meshfile]\n", argv[0]);
				return -1;
		}
	}
...

...
  fclose(fp_input);
  fclose(fp_mesh);
...

...
}
```
