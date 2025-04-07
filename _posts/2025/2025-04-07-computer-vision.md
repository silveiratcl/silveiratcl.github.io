---
title: Visão computacional
date: 2025-04-07 12:45:00 +/-TTTT
categories: [COMPUTER VISION, MACHINE LEARNING, PYTHON]
tags:  [machine learning, python, yolo, espécies invasoras]     # TAG names should always be lowercase
image:
  path: /assets/img/2025-04-07-header.png
---

# **Visão Computacional Contra Espécies Invasoras: Identificando Coral-Sol com YOLOv8**  

Imagine monitorar recifes de coral manualmente, mergulhando em águas profundas ou analisando horas de vídeo subaquático. Agora, pense em automatizar esse processo com **inteligência artificial**, acelerando a detecção de espécies invasoras como o **coral-sol (Tubastraea coccinea)**. Foi exatamente isso que exploramos em nosso projeto de visão computacional, usando **YOLOv8** para identificar e contar colônias dessa espécie em imagensubaquática.  

Neste post, vou compartilhar os desafios, resultados e lições aprendidas de um projeto da Disciplina Visão Computacional (INE410121 - VISÃO COMPUTACIONAL) ministrada pelo professor Aldo von Wangenheim. 

---  

## **O Problema: Coral-Sol e a Invasão Silenciosa**  

O coral-sol é uma espécie invasora que se espalhou rapidamente pelo Atlântico, competindo com espécies nativas e alterando ecossistemas marinhos. Tradicionalmente, seu monitoramento é feito por:  
- **Mergulhadores** (caro e limitado pela logística);  
- **ROVs (Veículos Subaquáticos Remotos)** (gera um volume enorme de imagens para análise manual).  

A pergunta que nos guiou foi: **Como a visão computacional pode tornar esse processo mais rápido e preciso?**  

---  

## **A Solução: YOLOv8 e um Banco de Dados Subaquático**  

### **1. Coleta e Anotação de Dados**  
Usamos imagens da **Reserva Biológica Marinha do Arvoredo (SC)**, capturadas com câmeras GoPro e Olympus. O desafio? Anotar manualmente **239 imagens** no [Roboflow](https://roboflow.com), marcando:  
- **Coral-sol** (nosso alvo principal);  
- **Algas turf**;  
- **Palythoa caribaeorum** (um coral nativo);  
- **Ouriços-do-mar**.  

![Exemplo de anotação no Roboflow](/assets/img/roboflow.png)

### **2. Treinamento do Modelo**  
Optamos pelo **YOLOv8**, um dos modelos mais eficientes para detecção em tempo real. Configuramos:  
- **50 épocas** de treinamento;  
- **Batch size = 64**;  
- **Imagens redimensionadas para 640x640 pixels**.  

Para melhorar a generalização, aplicamos **data augmentation** (rotações, ajuste de brilho, cortes aleatórios).  

---  

## **Resultados: Onde o Modelo Acertou (e Errou)**  

### **Desempenho Geral**  

| Classe                | Precisão | Recall    | mAP50  |  
| Tubastraea coccinea   | 0.607    | 0.716     | 0.676  |  
| Algae turf            | 0.404    | 0.200     | 0.193  |  
| Palythoa caribaeorum  | 0.341    | 0.278     | 0.246  |  
| Sea urchin            | 0.662    | 0.737     | 0.733  |  

## Tables

| Company                      | Contact          | Country |
| :--------------------------- | :--------------- | ------: |
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    |      UK |
| Magazzini Alimentari Riuniti | Giovanni Rovelli |   Italy |



O modelo teve **bons resultados para coral-sol (mAP50 = 0.676)**, mas:  
✅ **Detectou bem colônias isoladas e maiores**;  
❌ **Teve falsos positivos** (confundiu fundo ou outras espécies com coral-sol);  
❌ **Subestimou colônias em imagens borradas ou com má iluminação**.  

---  

## **Desafios e Lições Aprendidas**  

1. **Desbalanceamento de Classes**  
   - Espécies raras (como algas turf) tiveram baixa acurácia. **Solução possível**: Mais dados ou oversampling.  

2. **Problemas com Imagens Subaquáticas**  
   - Água turva e variação de luz afetaram a detecção. **Ideia para futuro**: Usar **pré-processamento** (ex.: algoritmos de correção de cor).  

3. **Contagem Imperfeita**  
   - O modelo **não substitui** totalmente a análise humana, mas **reduz drasticamente o tempo de triagem**.  

---  

## **Próximos Passos: O Futuro do Monitoramento Automatizado**  

- **Testar em outros habitats** (plataformas de petróleo, onde o coral-sol é comum);  
- **Explorar segmentação por instância** (ex.: Mask R-CNN) para colônias sobrepostas;  
- **Integrar drones submarinos** para captura contínua de imagens.  

---  

## **Conclusão: IA a Serviço da Conservação**  

Este projeto mostrou que **a visão computacional já é viável para monitoramento ambiental**, mesmo com desafios como imagens subaquáticas complexas. Ainda há espaço para melhorias, mas a automação pode **revolucionar** a gestão de espécies invasoras, tornando-a **mais rápida, barata e escalável**.  



**Dale!** 🚀  

---  

### **Referências**  
- Creed et al. (2017). *The Sun-Coral Project*. Management of Biological Invasions.  
- Beijbom et al. (2015). *Automated Annotation of Benthic Survey Images*. PLOS ONE.  
- [Roboflow](https://roboflow.com) – Ferramenta para anotação e aumento de dados.  

---  


