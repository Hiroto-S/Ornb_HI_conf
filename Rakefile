# -*- coding: utf-8 -*-
file = 'thesis'
KEY_WORD_FOR_HEAD1 = '\title{}' # '\auth{bob}'

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
\etitle{ Learning Process by Knowledge Construction System 'ornb' }
% PM makes new seminar system

%著者英文名
\eauthor{
Kono Hiroto\thanks{Graduate school of Science and Technology, Kwansei Gakuin Univ.},　
Satoshi Fukumori\thanks{Department of Informatics, Kwansei Gakuin Univ. }　and
Shigeto R. Nishitani\addtocounter{footnote}{-1}\footnotemark
}
EOS

$head2 = <<'EOS'
\end{abstract}

\begin{keyword}
learning support, educational system, problem finding
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
              "platex #{t_file}.tex",
              "dvipdfmx #{t_file}.dvi",
              "open #{t_file}.pdf",
              "cp thesis_final.pdf hi_shinsei_928.pdf"
             ]
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

    line.gsub!(KEY_WORD_FOR_HEAD1, $head1)
    line.gsub!('\section{abstract}','\begin{abstract}')
    line.gsub!('\section{Introduction}', $head2)
    line.gsub!('{table}', '{table*}')
#    line.gsub!('\section','\chapter')
#    line.gsub!('\subsection','\section')
#    line.gsub!('\subsubsection','\subsection')
  end
  return new_line
end

