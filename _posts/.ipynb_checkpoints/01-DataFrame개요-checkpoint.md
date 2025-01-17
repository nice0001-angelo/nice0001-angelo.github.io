---
layout: post
title:01.DataFrame
---


{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 데이터프레임 개요"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Pandas 란?\n",
    "\n",
    "- 데이터 분석, 처리 등을 쉽게 하도록 만들어진 python package\n",
    "- 대용량 데이터를 보다 쉽고 안정적으로 처리할 수 있다"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Pandas 설치\n",
    "\n",
    "> pip install pandas"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Pandas의 자료구조\n",
    "**DataFrame**\n",
    "\n",
    "- 열과 행으로 구성된 엑셀 표와 같은 구조\n",
    "- 각 행과 열을 이루는 단위는 Series라는 객체\n",
    "- Series가 모여서 DataFrame가 됨(Series는 엑셀의 세로 셀)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Series\n",
    "- index와 value로 구성된 numpy 배열의 확장 객체"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "-------------------------\n",
    "## #01. 필요한 모듈 참고"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "# pandas 모듈에서 Series 클래스 가져오기\n",
    "from pandas import Series"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "---------------------------\n",
    "## #02. Series 객체 살펴보기\n",
    "\n",
    "### **Series 객체생성**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    10\n",
       "1    30\n",
       "2    50\n",
       "3    70\n",
       "4    90\n",
       "dtype: int64"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 기본 Series 만들기\n",
    "# -> List 자료형을 가공하여 생성된 데이터 구조가 Series임\n",
    "# list -> numpy array --> Series : 파이썬의 리스트를 numpy array를 가공한게 Series 임 : 참고로 파이썬의 리스트는 원래 배열이라고 생각 하면 됨\n",
    "# numpy에서 사용하는 함수는 기본으로 pandas에 다 들어가 있음\n",
    "items = [10,30,50,70,90]\n",
    "column = Series(items)\n",
    "column"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "10\n",
      "50\n",
      "90\n"
     ]
    }
   ],
   "source": [
    "# -> 인덱스를 활용한 개별 값 확인\n",
    "print(column[0])\n",
    "print(column[2])\n",
    "print(column[4])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([10, 30, 50, 70, 90], dtype=int64)"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 시리즈의 값들만 추출\n",
    "column.values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "numpy.ndarray"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 타입을 확인하면 Numpy 배열임을 알 수 있다.\n",
    "type(column.values)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[10, 30, 50, 70, 90]"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# --> 시리즈의 값들을 저장하고 있는 numpy 배열을 list로 변환\n",
    "value_list = list(column.values)\n",
    "value_list"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "RangeIndex(start=0, stop=5, step=1)"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 시리즈의 색인(index)만 추출\n",
    "column.index"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "pandas.core.indexes.range.RangeIndex"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 색인들의 타입 확인\n",
    "type(column.index)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0, 1, 2, 3, 4]"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 시리즈의 색인(index)을 list로 변환\n",
    "list(column.index)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### **조건검색**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2    50\n",
       "3    70\n",
       "4    90\n",
       "dtype: int64"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 특정 조건에 맞는 항목들만 추출\n",
    "# -> 이름[이름에 대한 조건식]\n",
    "# -> 30초과인 항목들만 추출\n",
    "in1 = column[column > 30]\n",
    "in1"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1    30\n",
       "2    50\n",
       "3    70\n",
       "dtype: int64"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# -> 70이하 and 10초과인 항목들만 추출\n",
    "in2 = column[column > 10][column<=70]\n",
    "in2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    10\n",
       "3    70\n",
       "4    90\n",
       "dtype: int64"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# -> 10이하 or 70이상인 항목들만 추출\n",
    "in3 = column[(column <= 10)|(column>=70)]\n",
    "in3"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### **인덱스를 직접 지정하기**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "토    290000\n",
       "일    310000\n",
       "dtype: int64"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "week1 = Series([290000,310000], index=['토','일'])\n",
    "week1"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "일    120000\n",
       "토    220000\n",
       "dtype: int64"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "week2 = Series([120000,220000], index=['일','토'])\n",
    "week2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "일    430000\n",
       "토    510000\n",
       "dtype: int64"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 시리즈 객체의 사칙연산\n",
    "# --> index가 동일한 항목끼리 연산이 수행된다.\n",
    "Result = week1 + week2\n",
    "Result"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.4"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
