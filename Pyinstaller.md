
To make your Python script ultra low resource consuming when compiled to an executable using PyInstaller, you can follow these steps:

1. **Optimize your code**: Ensure that your code is as efficient as possible. This includes removing unnecessary imports, optimizing loops, and using efficient data structures.

2. **Use a minimal base image**: PyInstaller supports a `--onefile` option that bundles everything into a single executable. This can be useful if you want to reduce the number of files that need to be distributed. However, if you're distributing an application that needs to be installed, using a `--onedir` or `--onefile --nowindow` might be more appropriate.

3. **Strip unnecessary debug information**: Debug information can be removed from the executable using the `--strip` option. This can significantly reduce the size of the executable.

4. **Use UPX**: UPX is a free, portable, extendable, high-performance executable packer for several executable formats. You can use PyInstaller's `--upx-dir` option to specify the path to the UPX executable. This can further reduce the size of the executable.

5. **Exclude unnecessary modules**: If you're using `PyInstaller` with the `--hidden-import` option, you can exclude modules that are not necessary for your application to run. This can help reduce the size of the executable.

Here's an example of how you might compile your script using PyInstaller with these optimizations:

```bash
pyinstaller --onefile --strip --upx-dir /path/to/upx your_script.py
```

Replace `/path/to/upx` with the actual path to your UPX executable and `your_script.py` with the name of your Python script.

By following these steps, you should be able to create an ultra low resource consuming executable for your Discord bot using PyInstaller. Remember that the final size of the executable will depend on the complexity of your code and the libraries you're using.