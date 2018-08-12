# 입력 파일이 여러개인 경우

입력 파일이 여러개인 경우는 [1개인 경우 예제](./01_Inputfile_Open.md)에서 option_list 리스트에 make_option함수를 통해 입력 받고자 하는 옵션을 추가 해주면 됩니다.

```R
#!/usr/bin/env Rscript

library(optparse)

option_list <- list (
    make_option(c("-i","--inp"), type='character', help="Input file path", default=NULL ,metavar="character"),
    make_option(c("-m","--mesh"), type='character', help="Input mesh path", default=NULL ,metavar="character")
);

opt_parser <- OptionParser(option_list=option_list);
opt <- parse_args(opt_parser);

if (is.null(opt$inp) & is.null(opt$mesh) ){
    print_help(opt_parser);
    stop("At least one argument must be supplied (input file).n", call.=FALSE);
}

inputfilepath = opt$inp;
meshfilepath = opt$mesh;

print(inputfilepath);
print(meshfilepath);

```
