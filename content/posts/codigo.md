---
title: "6 - Codigo"
date: 2020-11-04T16:10:21-03:00
draft: true
---
	// biblioteca
	#include <LiquidCrystal.h>
	
	//definindo o pino do buzzer
	int buzzer = 9;
	
	//definindo o incio dos horarios
	int segundos = 0;
	int minutos = 0;
	int horas = 0;
	
	//definindo notas musicais
	#define sol 392
	#define la  440
	#define si  494
	#define do_1  263
	#define re  294
	#define mi  330
	#define fa  349
	
	// inicializacao dos pinos pela biblioteca
	LiquidCrystal lcd(7, 6, 5, 4, 3, 2);
	
	void setup()
	{
	  //iniciando o buzzer
	  pinMode(buzzer, OUTPUT);
	   
	  // definindo o tamanho do lcd com no numero de colunas e linhas
	  lcd.begin(16, 2);
	  Serial.begin(9600);
	}
	
	void loop()
	{
	  //organizando o cronometro para parar em 60
	  // pra acelerar e so multiplicar o millis
	  segundos = ((millis()) / 1000)-(minutos*60)-(horas*3600);
	 
	  //Onde vai aparecer a mensagem;
	  lcd.setCursor(0,0);
	 
	  // mensagem
	  lcd.print("Relogio");
	 
	  //onde vai aparecer a mensagem;
	  lcd.setCursor(0,1);
	 
	  //quando as horas forem igual a 24, o cronometro reinicia
	  if(horas > 23)
	  {
	   
	    horas = 0;
	    minutos = 0;
	    segundos = 0;
	 
	   //limpa tela
	   lcd.clear();
	  }
	 
	  // mostrando o cronometro em horas
	  lcd.print(horas);
	 
	  lcd.print(":");//separacao
	
	 
	  //quando os minutos forem igual a 60, o cronometro reinicia
	  if(minutos > 59)
	  {
	    minutos = 0;
	    segundos = 0;
	    horas = horas + 1;
	
	    //limpa tela  
	    lcd.clear();
	  }
	  // mostrando o cronometro em minutos
	  lcd.print(minutos);
	 
	  lcd.print(":");//separacao
	   
	  //quando os segundos forem igual a 60, o cronometro reinicia
	  if(segundos > 59)
	  {
	    minutos = minutos + 1;
	    segundos = 0;
	
	    //limpa tela  
	    lcd.clear();
	  }
	  //mostrando o cronometro em segundos
	  lcd.print(segundos);
	
	  //quando o relogio batar em 6 horas um despertador toca
	  if(horas == 6 && minutos == 0)
	  {
	    tone(buzzer,sol,500);
	    delay(500);
	    tone(buzzer,la,500);
	    delay(500);
	    tone(buzzer,si,500);
	    delay(500);
	    tone(buzzer,do_1,500);
	    delay(500);
	    tone(buzzer,re,500);
	    delay(500);
	    tone(buzzer,mi,500);
	    delay(500);
	    tone(buzzer,fa,500);
	    delay(500);
	   
	    //a musica para sozinha em 3,5 segundos
	    noTone(buzzer);
	  }
	  Serial.print(horas);
	  Serial.print(":");
	  Serial.print(minutos);
	  Serial.print(":");
	  Serial.println(segundos);
	}
	