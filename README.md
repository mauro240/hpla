import time
import pygame
import sys

# Inicializar Pygame
pygame.init()

# Configuración de la pantalla
ANCHO_PANTALLA = 640
ALTO_PANTALLA = 480

# Colores
NEGRO = (0, 0, 0)
BLANCO = (255, 255, 255)

# Fuente
fuente = pygame.font.Font(None, 74)

pantalla = pygame.display.set_mode((ANCHO_PANTALLA, ALTO_PANTALLA))
pygame.display.set_caption("Temporizador de alarma")

def mostrar_tiempo_restante(segundos_restantes):
    pantalla.fill(NEGRO)
    minutos_restantes = segundos_restantes // 60
    segundos_restantes = segundos_restantes % 60
    tiempo_formateado = f"{minutos_restantes:02d}:{segundos_restantes:02d}"
    texto = fuente.render(tiempo_formateado, True, BLANCO)
    rect_texto = texto.get_rect(center=(ANCHO_PANTALLA // 2, ALTO_PANTALLA // 2))
    pantalla.blit(texto, rect_texto)
    pygame.display.flip()

    return minutos_restantes, segundos_restantes

min, seg = mostrar_tiempo_restante(34)

print(min, seg)

def alarma(segundos):
    tiempo_inicial = time.time()
    tiempo_transcurrido = 0

    while tiempo_transcurrido < segundos:
        for evento in pygame.event.get():
            if evento.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        tiempo_actual = time.time()
        tiempo_transcurrido = tiempo_actual - tiempo_inicial
        segundos_restantes = int(segundos - tiempo_transcurrido)

        minutos_restantes, segundos_restantes = mostrar_tiempo_restante(segundos - tiempo_transcurrido)
        tiempo_transcurrido = time.time() - tiempo_inicial
        pygame.time.delay(100)

    # Aquí puedes agregar el código para la alarma (sonido, notificación, etc.)

while True:
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
alarma(50)

while True:
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            pygame.quit()
            sys.exit()# hpla
