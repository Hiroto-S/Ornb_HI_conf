# -*- coding: utf-8 -*-
file = 'thesis'

desc "platex"
task :platex do
  lines = File.readlines("#{file}.tex")
  t_file = 'thesis_final'
  lines = convert_thesis(lines)
  File.open("#{t_file}.tex",'w') do |f|
    lines.each{|line| f.print line }
  end
  system "platex #{file}"
  commands = ["platex #{t_file}.tex",
              "bibtex #{t_file}.tex",
              "platex #{t_file}.tex",
              "dvipdfmx #{t_file}.dvi",
              "open #{t_file}.pdf"]
  commands.each{|com| system com}
end

def convert_thesis(lines)
  head = <<'EOS'
\documentclass{hissymp}
\usepackage[dvipdfmx]{graphicx}
EOS
  new_line = [head]
  lines[4..-1].each do |line|
    if line.match(/\\tableofcontents\n/)
      line = "\\tableofcontents\n\\listoftables\n\\listoffigures\n\\pagebreak\n"
      p line
    end
    new_line << line
  end

  new_line.each do |line|
#    line.gsub!('\section','\chapter')
#    line.gsub!('\subsection','\section')
#    line.gsub!('\subsubsection','\subsection')
  end
  return new_line
end
