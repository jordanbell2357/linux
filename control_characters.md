# Control characters

<p>ANSI X3.4-1977. <a href="https://nvlpubs.nist.gov/nistpubs/Legacy/FIPS/fipspub1-2-1977.pdf">American National Standard Code for Information Interchange</a></p>

<blockquote>
<strong>Control Character.</strong> A character whose occurrence in a
particular context initiates, modifies, or stops an action that affects the recording, processing, transmission, or interpretation of data. (p. 10)
</blockquote>

<blockquote>
<strong>1/11 ESC (Escape).</strong> A control character intended to
provide supplementary characters (code extension).
The Escape character itself is a prefix affecting the
interpretation of a limited number of contiguous bit
patterns. The effect of this character is described in
American National Standard X3.41-1974. (p. 11)
</blockquote>

<a href="https://ecma-international.org/publications-and-standards/standards/ecma-48/">ECMA-48</a>

<a href="https://vt100.net/docs/vt100-ug/chapter3.html#T3-5">VT100 User Guide, S3.3.6</a>

> CTRL (Control) – The CTRL key is used in conjunction with other keys on the keyboard to generate control codes. If the CTRL key is held down when any of the keys in Table 3-5 are typed,
  the code actually transmitted is in the range 0008-0378. 

<table>
<caption>Table 3-5 Control Codes Generated</caption>  
  <thead>
  <tr>
    <th>Key Pressed with CTRL key down (shifted or unshifted)</th>
    <th>Octal Code Transmitted</th>
    <th>Function Mnemonic</th>
  </tr></thead>
<tbody>
  <tr>
    <td>Space Bar</td>
    <td>000</td>
    <td>NUL</td>
  </tr>
  <tr>
    <td>A</td>
    <td>001</td>
    <td>SOH</td>
  </tr>
  <tr>
    <td>B</td>
    <td>002</td>
    <td>STX</td>
  </tr>
  <tr>
    <td>C</td>
    <td>003</td>
    <td>ETX</td>
  </tr>
  <tr>
    <td>D</td>
    <td>004</td>
    <td>EOT</td>
  </tr>
  <tr>
    <td>E</td>
    <td>005</td>
    <td>ENQ</td>
  </tr>
  <tr>
    <td>F</td>
    <td>006</td>
    <td>ACK</td>
  </tr>
  <tr>
    <td>G</td>
    <td>007</td>
    <td>BELL</td>
  </tr>
  <tr>
    <td>H</td>
    <td>010</td>
    <td>BS</td>
  </tr>
  <tr>
    <td>I</td>
    <td>011</td>
    <td>HT</td>
  </tr>
  <tr>
    <td>J</td>
    <td>012</td>
    <td>LF</td>
  </tr>
  <tr>
    <td>K</td>
    <td>013</td>
    <td>VT</td>
  </tr>
  <tr>
    <td>L</td>
    <td>014</td>
    <td>FF</td>
  </tr>
  <tr>
    <td>M</td>
    <td>015</td>
    <td>CR</td>
  </tr>
  <tr>
    <td>N</td>
    <td>016</td>
    <td>SO</td>
  </tr>
  <tr>
    <td>O</td>
    <td>017</td>
    <td>SI</td>
  </tr>
  <tr>
    <td>P</td>
    <td>020</td>
    <td>DLE</td>
  </tr>
  <tr>
    <td>Q</td>
    <td>021</td>
    <td>DC1 or XON</td>
  </tr>
  <tr>
    <td>R</td>
    <td>022</td>
    <td>DC2</td>
  </tr>
  <tr>
    <td>S</td>
    <td>023</td>
    <td>DC3 or XOFF</td>
  </tr>
  <tr>
    <td>T</td>
    <td>024</td>
    <td>DC4</td>
  </tr>
  <tr>
    <td>U</td>
    <td>025</td>
    <td>NAK</td>
  </tr>
  <tr>
    <td>V</td>
    <td>026</td>
    <td>SYN</td>
  </tr>
  <tr>
    <td>W</td>
    <td>027</td>
    <td>ETB</td>
  </tr>
  <tr>
    <td>X</td>
    <td>030</td>
    <td>CAN</td>
  </tr>
  <tr>
    <td>Y</td>
    <td>031</td>
    <td>EM</td>
  </tr>
  <tr>
    <td>Z</td>
    <td>032</td>
    <td>SUB</td>
  </tr>
  <tr>
    <td>[</td>
    <td>033</td>
    <td>ESC</td>
  </tr>
  <tr>
    <td>\</td>
    <td>034</td>
    <td>FS</td>
  </tr>
  <tr>
    <td>]</td>
    <td>035</td>
    <td>GS</td>
  </tr>
  <tr>
    <td>~</td>
    <td>036</td>
    <td>RS</td>
  </tr>
  <tr>
    <td>?</td>
    <td>037</td>
    <td>US</td>
  </tr>
</tbody></table>
