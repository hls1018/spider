#!/usr/bin/env python
# -*- coding: utf-8 -*-
import os
import urllib2
import urllib
from bs4 import  BeautifulSoup
import time
import lxml
import re
year_list=[]
word_disc ={}
valuse=1

def write_mt_html(page):

    with open('mt.html','w') as mawr:
        mawr.write(page)


def number_of_words(page):

    wjobj = BeautifulSoup(page, 'lxml')

    p_list = wjobj.select('#mw-content-text > div > p')

    for p_item in p_list:
            result_list = re.findall(r'[a-zA-Z]+', str(p_item))
            for worditem in result_list:
                if len(worditem)>1:
                   if word_disc.has_key(worditem):
                       word_disc[worditem] =valuse+1
                   else:
                       word_disc[worditem] = 1

    for  keys in word_disc.keys():

        with open('mt_word.txt','a+') as word_wr:
            word_wr.write(keys + '  ' + str(word_disc[keys]) + '\r\n')


def Extraction_of_year(page):

    wjobj = BeautifulSoup(page, 'lxml')

    years = wjobj.select('#mw-content-text > div > p')

    for item in years:
        result_list = re.findall(r'\d+', str(item))
        for yearitem in  result_list:
            if len(yearitem) ==4:
                year_list.append(yearitem)

    for year_items in sorted(year_list):
        with open('mt_year.txt','a+') as mtyearwr:
            mtyearwr.write(year_items +'\r\n')

def main(urls):

    page=urllib.urlopen(urls).read()

    #将网页写入mt.html
    write_mt_html(page)

    #获取单词
    #number_of_words(page)

    #获取网页中的年份
    Extraction_of_year(page)


if __name__ == '__main__':
    urls = 'https://en.wikipedia.org/wiki/Machine_translation'
    main(urls)
