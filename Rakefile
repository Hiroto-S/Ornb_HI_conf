# -*- coding: utf-8 -*-
file = 'thesis'

$head0 = <<'EOS'
\documentclass{hissymp}
\usepackage[dvipdfmx]{graphicx}
EOS

$head1 = <<'EOS'
%和文タイトル
\jtitle{知識構築システムornbを利用した学習過程の考察}
%著者日本名
\jauthor{
河野大登\thanks{関西学院大学大学院　理工学研究科}　　
福森聡\thanks{関西学院大学　理工学部}
西谷滋人\addtocounter{footnote}{-1}\footnotemark
}

%英文タイトル
\etitle{hoge hoge}

%著者英文名
\eauthor{
Kono Hiroto\thanks{Graduate school of science and engineering, Kwansei Gakuin Univ.},　
Satoshi Fukumori\thanks{Department of Informatics, Kwansei Gakuin Univ. }　and
Shigeto R. Nishitan\addtocounter{footnote}{-1}\footnotemark
}
EOS

$head2 = <<'EOS'
\end{abstract}

\begin{keyword}
keyword 1, keyword 2, keyword 3, keyword 4, keyword 5
\end{keyword}

\maketitle
\section{Introduction}
EOS
desc "platex"
task :platex do
  lines = File.readlines("#{file}.tex")
  t_file = 'thesis_final'
  lines = convert_thesis(lines)
  File.open("#{t_file}.tex",'w') do |f|
    lines.each{|line| f.print line }
  end

  commands = ["platex #{t_file}.tex",
              "bibtex #{t_file}.tex",
              "platex #{t_file}.tex",
              "dvipdfmx #{t_file}.dvi",
              "open #{t_file}.pdf"]
  commands.each{|com| system com}
end

def convert_thesis(lines)
  new_line = [$head0]
  lines[4..-1].each do |line|
    if line.match(/\\tableofcontents\n/)
      line = "\\tableofcontents\n\\listoftables\n\\listoffigures\n\\pagebreak\n"
      p line
    end
    new_line << line
  end

  new_line.each do |line|
    line.gsub!('\author{bob}', $head1)
    line.gsub!('\section{abstract}','\begin{abstract}')
    line.gsub!('\section{Introduction}', $head2)
#    line.gsub!('\section','\chapter')
#    line.gsub!('\subsection','\section')
#    line.gsub!('\subsubsection','\subsection')
  end
  return new_line
end

