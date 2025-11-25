from graphviz import Digraph

def gerar_diagrama():
    dot = Digraph("UML_Atividade_Vazamento_Oleo")
    dot.attr(rankdir="TB", size="8,10")

    # Nó inicial
    dot.node("inicio", shape="circle", label="", style="filled", fillcolor="black")

    # Evento inicial
    dot.node("inicio_oleo", "Início derramamento de óleo", shape="box", color="blue")

    # Monitoramento e identificação
    dot.node("monitor", "Monitoramento (Satélite/Aeronave)", shape="box", color="orange")
    dot.node("alerta", "Identificação e Alerta do derrame", shape="box", color="blue")

    # Ambiente e dispersão
    dot.node("ambiente", "Ambiente Marinho (Vento, corrente)", shape="box", color="yellow")
    dot.node("dispersao", "Dispersão e Movimentação do óleo", shape="box", color="blue")

    # Resposta e limpeza
    dot.node("equipe_limpeza", "Equipe de Limpeza", shape="box", color="yellow")
    dot.node("acao_limpeza", "Ação de Limpeza da costa/Praias", shape="box", color="blue")
    dot.node("contencao", "Ação de contenção (Barcos/Barreiras)", shape="box", color="orange")
    dot.node("equipe_resposta", "Equipe de Resposta", shape="box", color="yellow")

    # Consequências
    dot.node("bio", "Consequência Biológica:\nMorte/Contaminação de Organismos", shape="box", color="orange")
    dot.node("ecosistema", "Ecossistema (Vida marinha, Aves)", shape="box", color="yellow")
    dot.node("econ", "Consequência Econômica:\nImpacto na pesca e Turismo", shape="box", color="orange")
    dot.node("comunidades", "Comunidades costeiras/Indústria", shape="box", color="yellow")

    # Monitoramento final
    dot.node("monitoramento_final", "Monitoramento de Recuperação Ambiental", shape="box", color="blue")
    dot.node("cientistas", "Cientistas/Órgãos Ambientais", shape="box", color="yellow")

    # Fim
    dot.node("fim", shape="doublecircle", label="", style="filled", fillcolor="black")
    dot.node("residuos", "Fim/Recuperação ou Resíduos persistentes", shape="box", color="green")

    # Fluxo principal
    dot.edges([
        ("inicio", "inicio_oleo"),
        ("inicio_oleo", "ambiente"),
        ("inicio_oleo", "monitor"),
        ("monitor", "alerta"),
        ("alerta", "bio"),
        ("bio", "ecosistema"),
        ("ecosistema", "econ"),
        ("econ", "comunidades"),
        ("comunidades", "contencao"),
        ("contencao", "equipe_resposta"),
        ("ambiente", "dispersao"),
        ("dispersao", "acao_limpeza"),
        ("acao_limpeza", "equipe_limpeza"),
        ("equipe_limpeza", "monitoramento_final"),
        ("monitoramento_final", "cientistas"),
        ("cientistas", "residuos"),
        ("residuos", "fim")
    ])

    # Exportar arquivo PNG
    output_path = "diagrama_atividade_vazamento_oleo"
    dot.render(output_path, format="png", cleanup=True)

    print(f"✅ Diagrama gerado com sucesso: {output_path}.png")


if __name__ == "__main__":
    gerar_diagrama()
