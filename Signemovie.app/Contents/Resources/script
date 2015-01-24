if !ARGV.empty?
  ffmpeg = Dir.pwd + "/ffmpeg"
  puts ffmpeg
  Dir.chdir(ARGV[0])

  files = []

  Dir.glob("*").sort.each do |file|
    if file.split(".").last.downcase == "jpg"
      files << file
    end
  end

  files.each_with_index do |file, index|
    File.rename(ARGV[0] + "/" + file, ARGV[0] + "/image" + index.to_s.rjust(Dir.glob("*").size.to_s.size, "0") + ".jpg")
  end

  File.delete(ARGV[0] + "/output.mpg") if File.exist?("output.mpg")

  fps = File.open(ARGV[0] + "/fps.txt").readline.to_i

  system ffmpeg + ' -t 20 -f image2 -r ' + fps.to_s + ' -loop 1 -i "image%0' + Dir.glob("*").size.to_s.size.to_s + 'd.jpg" -r 30 "out.mov"'
end