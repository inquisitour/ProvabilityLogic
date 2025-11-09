\documentclass[11pt,a4paper]{article}
\usepackage[utf8]{inputenc}
\usepackage[margin=2.5cm]{geometry}
\usepackage{amsmath,amssymb,amsthm}
\usepackage{tikz}
\usetikzlibrary{arrows.meta,positioning,shapes,calc}
\usepackage{xcolor}
\usepackage{tcolorbox}
\usepackage{booktabs}
\usepackage{enumitem}
\usepackage{fancyhdr}

% Colors
\definecolor{glcolor}{RGB}{0,102,204}
\definecolor{glicolor}{RGB}{204,0,102}
\definecolor{headercolor}{RGB}{51,51,51}

% Header/Footer
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\small\textcolor{headercolor}{GL and GL+I Frame Properties}}
\fancyhead[R]{\small\textcolor{headercolor}{Pratik Deshmukh, TU Wien}}
\fancyfoot[C]{\thepage}
\renewcommand{\headrulewidth}{0.5pt}

% Title formatting
\title{\vspace{-1cm}\textbf{\LARGE Frame Properties of GL and GL+I}\\\vspace{0.3cm}\large A Technical Reference for Modal Provability Logic Extensions}
\author{Pratik Deshmukh\\MSc Logic and Computation, TU Wien}
\date{November 2025}

\begin{document}

\maketitle
\thispagestyle{fancy}

\begin{tcolorbox}[colback=blue!5!white,colframe=glcolor,title=Quick Reference]
\textbf{GL}: K4 + Irreflexivity + Well-foundedness\\
\textbf{GL+I}: Bi-modal (GL for $\square$, K+Trans for I, with $R_\square \subseteq R_I$)
\end{tcolorbox}

\section{Standard GL (Gödel-Löb Provability Logic)}

\subsection{Frame Definition}
A \textbf{GL frame} is a structure $\mathcal{F} = \langle W, R \rangle$ where:
\begin{itemize}[leftmargin=*]
\item $W$ is a non-empty finite set of possible worlds
\item $R$ is a binary accessibility relation on $W$
\end{itemize}

\subsection{Frame Conditions}

\begin{tcolorbox}[colback=gray!5!white,colframe=gray!75!black]
\textbf{T1. Transitivity}
$$\forall w, v, u \in W: (wRv \land vRu) \rightarrow wRu$$
\textit{Validates axiom \textbf{4}}: $\square A \rightarrow \square\square A$
\end{tcolorbox}

\begin{tcolorbox}[colback=gray!5!white,colframe=gray!75!black]
\textbf{T2. Irreflexivity}
$$\forall w \in W: \neg(wRw)$$
\textit{Consequence}: $\square A \rightarrow A$ is \textbf{not} valid (distinguishes GL from S4)
\end{tcolorbox}

\begin{tcolorbox}[colback=gray!5!white,colframe=gray!75!black]
\textbf{T3. Conversely Well-Founded}
$$\text{No infinite sequence: } \ldots R w_2 R w_1 R w_0$$
\textit{Validates \textbf{Löb's axiom}}: $\square(\square A \rightarrow A) \rightarrow \square A$
\end{tcolorbox}

\textbf{Note}: In finite frames, T2 + T1 automatically implies T3.

\subsection{Truth Conditions}
For model $\mathcal{M} = \langle W, R, V \rangle$ and world $w \in W$:
$$\mathcal{M}, w \models \square A \quad\text{iff}\quad \forall v \in W: wRv \text{ implies } \mathcal{M}, v \models A$$

\subsection{Axiomatization}
GL extends classical propositional logic with:
\begin{itemize}[leftmargin=*]
\item \textbf{K}: $\square(A \rightarrow B) \rightarrow (\square A \rightarrow \square B)$
\item \textbf{4}: $\square A \rightarrow \square\square A$
\item \textbf{GL}: $\square(\square A \rightarrow A) \rightarrow \square A$
\item \textbf{Nec}: From $\vdash A$, infer $\vdash \square A$
\end{itemize}

\section{GL+I (Extended System with Interface Operator)}

\subsection{Frame Definition}
A \textbf{GL+I frame} is a triple $\mathcal{F} = \langle W, R_\square, R_I \rangle$ where:
\begin{itemize}[leftmargin=*]
\item $W$ is a non-empty finite set of possible worlds
\item $R_\square$ is the provability accessibility relation (GL conditions)
\item $R_I$ is the interface accessibility relation (new)
\end{itemize}

\subsection{Frame Conditions}

\textbf{For $R_\square$ (provability relation)}: Standard GL conditions (Transitive, Irreflexive, Well-founded)

\textbf{For $R_I$ (interface relation)}:

\begin{tcolorbox}[colback=glicolor!5!white,colframe=glicolor]
\textbf{I1. Transitivity}
$$\forall w, v, u \in W: (wR_Iv \land vR_Iu) \rightarrow wR_Iu$$
\textit{Required for axiom \textbf{I2}}: $IA \rightarrow IIA$
\end{tcolorbox}

\begin{tcolorbox}[colback=red!10!white,colframe=red!75!black,title=\textbf{CRITICAL CONSTRAINT}]
\textbf{I2. Inclusion}
$$\forall w, v \in W: wR_\square v \rightarrow wR_Iv$$
\textit{Required for axiom \textbf{I3}}: $\square A \rightarrow IA$\\
\textbf{Meaning}: Every provability arrow is also an interface arrow
\end{tcolorbox}

\begin{tcolorbox}[colback=glicolor!5!white,colframe=glicolor]
\textbf{I3. Irreflexivity (Optional)}
$$\forall w \in W: \neg(wR_Iw)$$
\textit{Status}: Not logically required, but simplifies frame theory
\end{tcolorbox}

\subsection{Truth Conditions}
For model $\mathcal{M} = \langle W, R_\square, R_I, V \rangle$ and world $w \in W$:
\begin{align*}
\mathcal{M}, w \models \square A &\quad\text{iff}\quad \forall v \in W: wR_\square v \text{ implies } \mathcal{M}, v \models A\\
\mathcal{M}, w \models IA &\quad\text{iff}\quad \forall v \in W: wR_Iv \text{ implies } \mathcal{M}, v \models A
\end{align*}

\subsection{Extended Axiomatization}
GL+I extends GL with three interface axioms:
\begin{itemize}[leftmargin=*]
\item \textbf{I1}: $I(A \rightarrow B) \rightarrow (IA \rightarrow IB)$ — Distribution
\item \textbf{I2}: $IA \rightarrow IIA$ — Self-reflection
\item \textbf{I3}: $\square A \rightarrow IA$ — Inclusion
\item \textbf{Nec$_I$}: From $\vdash A$, infer $\vdash IA$
\end{itemize}

All GL axioms and theorems are preserved.

\subsection{Bi-Modal Structure}
GL+I is a \textbf{bi-modal logic} with independent modalities coupled through inclusion:

\begin{center}
\begin{tabular}{@{}lll@{}}
\toprule
\textbf{Operator} & \textbf{Base Logic} & \textbf{Frame Type} \\
\midrule
$\square$ (Box) & GL & Trans + Irref + WF \\
$I$ (Interface) & K + Trans & Trans + ($R_\square \subseteq R_I$) \\
\bottomrule
\end{tabular}
\end{center}

\section{Key Differences and Relationships}

\subsection{Comparison with Standard Modal Logics}

\begin{center}
\begin{tabular}{@{}lcccl@{}}
\toprule
\textbf{Logic} & \textbf{Refl.} & \textbf{Trans.} & \textbf{Sym.} & \textbf{Other} \\
\midrule
K & — & — & — & Minimal \\
K4 & — & \checkmark & — & — \\
S4 & \checkmark & \checkmark & — & — \\
S5 & \checkmark & \checkmark & \checkmark & Equivalence \\
\textcolor{glcolor}{\textbf{GL}} & \textcolor{red}{$\times$} & \checkmark & — & + WF \\
\textcolor{glicolor}{\textbf{GL+I ($R_\square$)}} & \textcolor{red}{$\times$} & \checkmark & — & + WF \\
\textcolor{glicolor}{\textbf{GL+I ($R_I$)}} & ? & \checkmark & — & + Incl \\
\bottomrule
\end{tabular}
\end{center}

\subsection{The Non-Collapse Property}

The inclusion $R_\square \subseteq R_I$ (strict subset) enables:

\begin{tcolorbox}[colback=green!5!white,colframe=green!50!black]
\textbf{Theorem}: There exist models where $IA \land \neg\square A$
\end{tcolorbox}

This demonstrates that \textbf{$I \neq \square$} (genuine expressiveness increase).

\section{Semantic Correspondences}

\subsection{Axiom-Frame Correspondence}

\begin{center}
\begin{tabular}{@{}ll@{}}
\toprule
\textbf{Axiom} & \textbf{Frame Property} \\
\midrule
K & No constraint \\
4 ($\square A \rightarrow \square\square A$) & Transitivity \\
T ($\square A \rightarrow A$) & Reflexivity \\
GL ($\square(\square A \rightarrow A) \rightarrow \square A$) & Well-foundedness \\
I2 ($IA \rightarrow IIA$) & Transitivity of $R_I$ \\
I3 ($\square A \rightarrow IA$) & $R_\square \subseteq R_I$ \\
\bottomrule
\end{tabular}
\end{center}

\subsection{Failed Correspondences}

\begin{itemize}[leftmargin=*]
\item $\square A \rightarrow IA$ does \textbf{not} imply $IA \rightarrow \square A$ (due to $R_\square \subseteq R_I$)
\item $IA \rightarrow A$ is \textbf{not valid} (due to non-reflexivity of $R_I$)
\end{itemize}

\section{Computational Properties}

\begin{center}
\begin{tabular}{@{}lll@{}}
\toprule
\textbf{Property} & \textbf{GL} & \textbf{GL+I} \\
\midrule
Decidability & \checkmark & \checkmark \\
Complexity & PSPACE-complete & PSPACE-complete \\
Finite Model Property & \checkmark & \checkmark \\
\bottomrule
\end{tabular}
\end{center}

\section{Summary}

\subsection{GL Frames}
\begin{itemize}[leftmargin=*]
\item \textbf{Base}: K4 + irreflexivity + well-foundedness
\item \textbf{Not S4/S5}: Lacks reflexivity
\item \textbf{Single modality}: $\square$ (provability)
\end{itemize}

\subsection{GL+I Frames}
\begin{itemize}[leftmargin=*]
\item \textbf{Dual accessibility}: $R_\square$ (GL), $R_I$ (K + Trans)
\item \textbf{Critical constraint}: $R_\square \subseteq R_I$ (enables non-collapse)
\item \textbf{Conservative}: All GL theorems preserved
\item \textbf{Decidable}: PSPACE-complete (same as GL)
\end{itemize}

\subsection{Philosophical Interpretation}

The frame structure formalizes:
$$\text{Truth (semantic)} \supset IA \text{ (structural alignment)} \supset \square A \text{ (formal provability)}$$

The \textbf{graduated relationship} between truth and provability is captured through dual accessibility relations, where interface alignment mediates between semantic validity and syntactic derivability.

\vspace{0.5cm}
\noindent\rule{\textwidth}{0.4pt}

\subsection*{References}
\begin{enumerate}[leftmargin=*]
\item Boolos, G. (1993). \textit{The Logic of Provability}. Cambridge University Press.
\item Solovay, R. M. (1976). Provability interpretations of modal logic. \textit{Israel Journal of Mathematics}, 25(3-4), 287-304.
\item Beklemishev, L. (2005). Provability algebras and proof-theoretic ordinals. \textit{Annals of Pure and Applied Logic}, 132(2-3), 155-201.
\end{enumerate}

\noindent\rule{\textwidth}{0.4pt}

\begin{center}
\textit{Document Status: Technical Reference v1.0 | November 2025}\\
\textit{MSc Thesis on GL Extensions, TU Wien}
\end{center}

\newpage

\section*{Visual Guide: Modal Logic Frame Hierarchy}

\subsection*{1. Basic Modal Frames}

\begin{center}
\begin{tikzpicture}[scale=1.2,
    world/.style={circle,draw,minimum size=0.7cm,font=\small},
    arrow/.style={-{Stealth[length=2mm]},thick}]
    
% K - No constraints
\node[font=\Large\bfseries] at (0,3.5) {K (Minimal)};
\node[world] (k1) at (0,2.5) {$w_1$};
\node[world] (k2) at (1.5,2.5) {$w_2$};
\node[world] (k3) at (0.75,1.5) {$w_3$};
\draw[arrow] (k1) -- (k2);
\draw[arrow] (k2) -- (k3);
\draw[arrow,bend left=30] (k1) to (k3);
\node[font=\small,text width=3cm,align=center] at (0.75,0.8) {No constraints\\Any relation};

% K4 - Transitive
\node[font=\Large\bfseries] at (5,3.5) {K4 (Transitive)};
\node[world] (t1) at (5,2.5) {$w_1$};
\node[world] (t2) at (6.5,2.5) {$w_2$};
\node[world] (t3) at (5.75,1.5) {$w_3$};
\draw[arrow] (t1) -- (t2);
\draw[arrow] (t2) -- (t3);
\draw[arrow,red,thick] (t1) to[bend left=20] (t3);
\node[font=\small,text width=3cm,align=center] at (5.75,0.8) {Transitive\\Red = implied};

% S4 - Reflexive + Transitive
\node[font=\Large\bfseries] at (10,3.5) {S4 (Refl + Trans)};
\node[world] (s1) at (10,2.5) {$w_1$};
\node[world] (s2) at (11.5,2.5) {$w_2$};
\draw[arrow,blue,thick] (s1) to[loop left] (s1);
\draw[arrow,blue,thick] (s2) to[loop right] (s2);
\draw[arrow] (s1) -- (s2);
\node[font=\small,text width=3cm,align=center] at (10.75,1.5) {Reflexive + Trans\\Blue = self-loops};

\end{tikzpicture}
\end{center}

\begin{center}
\begin{tikzpicture}[scale=1.2,
    world/.style={circle,draw,minimum size=0.7cm,font=\small},
    arrow/.style={-{Stealth[length=2mm]},thick}]

% S5 - Equivalence
\node[font=\Large\bfseries] at (2.5,3.5) {S5 (Equivalence)};
\node[world] (e1) at (1.5,2.5) {$w_1$};
\node[world] (e2) at (3.5,2.5) {$w_2$};
\draw[arrow,blue,thick] (e1) to[loop left] (e1);
\draw[arrow,blue,thick] (e2) to[loop right] (e2);
\draw[arrow,bend left=20] (e1) to (e2);
\draw[arrow,bend left=20] (e2) to (e1);
\node[font=\small,text width=4cm,align=center] at (2.5,1.3) {Refl + Trans + Symmetric\\All worlds see each other};

% GL - Irrefl + Trans + WF
\node[font=\Large\bfseries,color=glcolor] at (8.5,3.5) {GL (Provability)};
\node[world,draw=glcolor,thick] (g1) at (8.5,2.5) {$w_0$};
\node[world,draw=glcolor,thick] (g2) at (7.5,1.5) {$w_1$};
\node[world,draw=glcolor,thick] (g3) at (9.5,1.5) {$w_2$};
\node[world,draw=glcolor,thick] (g4) at (8.5,0.5) {$w_3$};
\draw[arrow,color=glcolor] (g1) -- (g2);
\draw[arrow,color=glcolor] (g1) -- (g3);
\draw[arrow,color=glcolor] (g2) -- (g4);
\draw[arrow,color=glcolor] (g3) -- (g4);
\node[font=\small,text width=4cm,align=center,color=glcolor] at (8.5,-0.5) {\textbf{Irreflexive + Trans + WF}\\No self-loops, finite depth};

\end{tikzpicture}
\end{center}

\subsection*{2. GL+I Extended Frame (Your System)}

\begin{center}
\begin{tikzpicture}[scale=1.5,
    world/.style={circle,draw,minimum size=0.8cm,font=\normalsize},
    provability/.style={-{Stealth[length=3mm]},very thick,color=glcolor},
    interface/.style={-{Stealth[length=3mm]},very thick,color=glicolor,dashed}]

\node[font=\Large\bfseries] at (4,4.5) {\textcolor{glicolor}{GL+I Frame Structure}};

% Worlds
\node[world,draw=glcolor,very thick] (w0) at (4,3.5) {$w_0$};
\node[world,draw=glcolor,very thick] (w1) at (2,2) {$w_1$};
\node[world,draw=glcolor,very thick] (w2) at (6,2) {$w_2$};
\node[world,draw=glcolor,very thick] (w3) at (2,0.5) {$w_3$};
\node[world,draw=glcolor,very thick] (w4) at (6,0.5) {$w_4$};

% Provability arrows (solid blue)
\draw[provability] (w0) -- node[left,font=\small] {$R_\square$} (w1);
\draw[provability] (w1) -- (w3);

% Interface arrows (dashed magenta) - includes all R_□ plus extra
\draw[interface] (w0) -- (w1);
\draw[interface] (w0) -- node[right,font=\small] {$R_I$ only} (w2);
\draw[interface] (w1) -- (w3);
\draw[interface] (w2) -- (w4);

% Legend
\node[font=\small,text width=6cm,align=left] at (4,-1) {
\textcolor{glcolor}{─── $R_\square$ (Provability)}: GL conditions\\
\textcolor{glicolor}{- - - $R_I$ (Interface)}: Includes all $R_\square$ + additional arrows\\
};

% Key property box
\node[draw=red,thick,text width=6cm,align=center,fill=red!10,rounded corners] at (4,-2.5) {
\textbf{Critical:} $R_\square \subseteq R_I$\\
Every solid arrow is also dashed\\
But NOT vice versa
};

\end{tikzpicture}
\end{center}

\subsection*{3. The Modal Logic Hierarchy}

\begin{center}
\begin{tikzpicture}[scale=1,
    logic/.style={rectangle,draw,rounded corners,minimum width=2cm,minimum height=0.8cm,align=center,font=\small},
    implies/.style={-{Stealth[length=2mm]},thick}]

% Top level
\node[logic,fill=blue!10] (k) at (5,8) {\textbf{K}\\Minimal};

% Second level
\node[logic,fill=blue!20] (k4) at (5,6.5) {\textbf{K4}\\+ Trans};

% Third level - branching
\node[logic,fill=glcolor!20] (gl) at (2,5) {\textbf{GL}\\+ Irref + WF};
\node[logic,fill=blue!30] (s4) at (8,5) {\textbf{S4}\\+ Refl};

% Fourth level
\node[logic,fill=blue!40] (s5) at (8,3.5) {\textbf{S5}\\+ Sym};

% Your system
\node[logic,fill=glicolor!30,very thick,draw=glicolor] (gli) at (2,3) {\textbf{GL+I}\\+ Interface\\+ $R_\square \subseteq R_I$};

% Arrows
\draw[implies] (k) -- (k4);
\draw[implies] (k4) -- (gl);
\draw[implies] (k4) -- (s4);
\draw[implies] (s4) -- (s5);
\draw[implies,color=glicolor,very thick] (gl) -- (gli);

% Side annotations
\node[font=\footnotesize,text width=3cm,align=left] at (0,5) {Irreflexive\\path};
\node[font=\footnotesize,text width=3cm,align=right] at (10.5,5) {Reflexive\\path};

% Bottom annotation
\node[draw,thick,rounded corners,fill=yellow!20,text width=10cm,align=center,font=\small] at (5,1.5) {
\textbf{Position of GL and GL+I}:\\
GL branches from K4 (adds irreflexivity, NOT reflexivity like S4)\\
GL+I extends GL (bi-modal: GL for $\square$, K+Trans for I)
};

\end{tikzpicture}
\end{center}

\subsection*{4. Non-Collapse Visualization}

\begin{center}
\begin{tikzpicture}[scale=1.3,
    world/.style={circle,draw=glicolor,very thick,minimum size=1cm,font=\normalsize},
    provability/.style={-{Stealth[length=3mm]},ultra thick,color=glcolor},
    interface/.style={-{Stealth[length=3mm]},ultra thick,color=glicolor}]

\node[font=\Large\bfseries,color=glicolor] at (4,4) {Example: $IA \land \neg\square A$};

\node[world,fill=yellow!20] (w0) at (4,2.5) {$w_0$};
\node[world,fill=green!20] (w1) at (2,1) {$w_1$};
\node[world,fill=green!20] (w2) at (6,1) {$w_2$};

\draw[provability] (w0) -- node[left,font=\small] {$R_\square$} (w1);
\draw[interface] (w0) -- (w1);
\draw[interface] (w0) -- node[right,font=\small] {$R_I$ only!} (w2);

\node[font=\small,text width=7cm,align=left] at (4,-0.5) {
If $A$ is true at both $w_1$ and $w_2$:\\
• $w_0 \models IA$ (all $R_I$-accessible satisfy $A$)\\
• $w_0 \not\models \square A$ (if further structure makes $\square A$ false)\\
\textbf{Result}: Interface alignment without provability!
};

\end{tikzpicture}
\end{center}

\end{document}